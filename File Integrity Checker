import hashlib
import os
import json
import time

# ===============================
# File Integrity Checker Program
# ===============================
# This tool monitors files for unauthorized changes by calculating
# their SHA-256 hash values and comparing them over time.
# Any modification triggers an alert.
# ===============================

# JSON file to store previously known hash values
HASH_STORE = "file_hashes.json"


def calculate_hash(file_path):
    """
    Calculate SHA-256 hash of a given file.

    This function reads the file in chunks to avoid memory issues
    and computes the hash value to uniquely represent the file's contents.

    Returns:
        str: SHA-256 hash in hexadecimal form
        None: If the file does not exist
    """
    sha256 = hashlib.sha256()

    try:
        with open(file_path, "rb") as f:
            # Read file in chunks of 4096 bytes
            while chunk := f.read(4096):
                sha256.update(chunk)

        return sha256.hexdigest()

    except FileNotFoundError:
        # Return None if the file is missing
        return None


def load_stored_hashes():
    """
    Load previously stored hash values from the JSON database.

    Returns:
        dict: A dictionary mapping file paths to their stored SHA-256 hashes.
    """
    if not os.path.exists(HASH_STORE):
        return {}  # No stored hashes yet

    with open(HASH_STORE, "r") as f:
        return json.load(f)


def save_hashes(hashes):
    """
    Save the updated hash dictionary back to the JSON database.

    Args:
        hashes (dict): File paths mapped to their latest known hash values.
    """
    with open(HASH_STORE, "w") as f:
        json.dump(hashes, f, indent=4)


def monitor_files(file_list, interval=10):
    """
    Monitor a list of files for integrity changes.

    Args:
        file_list (list): List of file paths to monitor.
        interval (int): Time (seconds) to wait between checks.

    Behavior:
        - Loads stored hash values.
        - Generates initial hashes for new files.
        - Continuously recalculates and compares hashes.
        - Alerts if any file changes or disappears.
    """
    stored_hashes = load_stored_hashes()

    # Initial hashing for new files
    for file in file_list:
        if file not in stored_hashes:
            file_hash = calculate_hash(file)
            if file_hash:
                stored_hashes[file] = file_hash
                print(f"[INIT] Stored hash for {file}: {file_hash}")

    save_hashes(stored_hashes)

    print("\n[STARTING MONITORING] Press Ctrl+C to stop.\n")

    try:
        while True:
            for file in file_list:
                current_hash = calculate_hash(file)
                stored_hash = stored_hashes.get(file)

                # If the file is deleted or missing
                if current_hash is None:
                    print(f"[WARNING] File missing: {file}")
                    continue

                # If file has changed
                if current_hash != stored_hash:
                    print(f"[ALERT] File modified: {file}")
                    print(f"Old hash: {stored_hash}")
                    print(f"New hash: {current_hash}\n")

                    # Update stored hash to new value
                    stored_hashes[file] = current_hash
                    save_hashes(stored_hashes)

                else:
                    print(f"[OK] No change detected: {file}")

            # Wait before next file check cycle
            time.sleep(interval)

    except KeyboardInterrupt:
        print("\nMonitoring stopped by user.")


if __name__ == "__main__":
    # Add the files you want to monitor here
    files_to_monitor = [
        "test1.txt",
        "test2.txt"
    ]

    # Start monitoring with a 5-second interval
    monitor_files(files_to_monitor, interval=5)
