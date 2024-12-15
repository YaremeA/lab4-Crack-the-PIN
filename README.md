# lab4-Crack-the-PIN

const crypto = require('crypto');

/**
 * Attempts to crack the MD5 hash of a 5-digit PIN.
 * @param {string} hash - The MD5 hash of the original 5-digit PIN.
 * @returns {string|null} - The original PIN if found, otherwise null.
 */
function crack(hash) {
    // Iterate through possible PINs (00000 to 99999)
    for (let pin = 0; pin < 99999; pin++) {
        // Format number as a 5-digit string
        const pinString = String(pin).padStart(5, '0');

        // Generate MD5 hash for the PIN
        const computedHash = crypto.createHash('md5').update(pinString).digest('hex');

        // Check for a match
        if (computedHash === hash) {
            return pinString; // Return matched PIN
        }
    }

    return null; // Return null if no match found
}

// Example usage:
const exampleHash = '827ccb0eea8a706c4c34a16891f84e7b'; // MD5 for "12345"
console.log(crack(exampleHash)); // Outputs: "12345"
