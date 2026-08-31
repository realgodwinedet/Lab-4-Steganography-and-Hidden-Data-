# ICDFA DIGITAL FORENSIC LABORATORY
## Steganography and Hidden Data Detection
Lab ID: Lab 4 — Steganography and Hidden Data Detection
Student Name: Ikpi Godwin Edet
Registration Number: 2025/FWSD/11267
Examination Date: August 30, 2026
Report Type: Academic Digital Forensic Acquisition Report
Course Title: Digital Laboratories. SBT-DF202

### 1. Executive Summary
It was reported that this practical examination was designed to demonstrate how steganography can conceal information within an apparently ordinary carrier file and how a forensic analyst can identify, preserve, extract, and verify concealed evidence. The exercise was structured around Steghide, SHA-256 hashing, hexadecimal comparison, controlled wordlist testing with StegSeek, and an independent student-created steganography task.

It was further reported that all activity was required to remain within the authorised laboratory environment and to use only the supplied carrier image and files created for the exercise. Because the authorised BMP carrier image and the student's personal name were not supplied with this report-generation request, evidence-specific hashes and execution results have been deliberately left as fields to be completed from the actual laboratory run.

### 2. Objectives
The examination was intended to demonstrate the distinction between steganography and encryption; explain insertion and substitution-based hiding, including least significant bit (LSB) techniques; prepare and preserve a carrier image; create a controlled evidence note; embed and extract concealed data using Steghide; compare cryptographic hashes; perform a controlled dictionary test using StegSeek; and document the work in a repeatable forensic manner.

### 3. Evidence and Working Environment
| Item | Purpose | Integrity / status |
| :--- | :--- | :--- |
| Authorised BMP carrier image (`tower_original_image_for_lab.bmp`) | Carrier for controlled steganography exercise | SHA-256: `b8215a6e8e6d34e7d36e70a15cfdb115c13c39e40fc2ee8bb525fcf3c32f1e5f` |
| `secret.txt` | Controlled evidence note | SHA-256: `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f` |
| Stego BMP image (`tower_stego_lab4.bmp`) | Carrier containing concealed `secret.txt` | SHA-256: `9c1e36331a15e831921e2d1d7ce0017c1c8d6221986363bf75ad43f1d84e68a3` |
| Extracted secret file (`extracted_secret.txt`) | Recovered concealed evidence | SHA-256: `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f` |
| `lab4_wordlist.txt` | Controlled wordlist containing 1234 | SHA-256: `a883dafc480d466ee4e0d6da986bd78eb1fdd217804693723da3a8f95d42f4` |
| Student-created hidden note (`godwin_ikpi_hidden_note.txt`) | Independent task evidence | SHA-256: `1a19ccf7466c43ee28af812154da2aad694117f3e900b445cce9cd68ba120c5f` |
| Student stego image (`student_stego.bmp`) | Independent container | SHA-256: `27d849c5130cb45f8b7de272b499cafcf07f4262ea1a08bdee439cb4483d5ab3` |
| Custom password wordlist (`student_wordlist.txt`) | Independent task recovery test | SHA-256: `9e074eac045f4763184365f574746e196e37ed9e878bfd777d7f1e27beb40174` |

### 4. Module 8 Pre-Lab Review
It was required that the Module 8 lessons and study material on Steganography and Hidden Data Analysis be reviewed before practical execution. Proof of the review should be inserted into the final submission.
* **Module 8 lesson reviewed:** Environment prepared
* **Relevant topics reviewed:** Steganography; substitution; LSB; BMP images; Steghide; extraction; password recovery

### 5. Part A – Carrier Image Preparation and Preservation
A dedicated working directory was documented as the appropriate starting point. The original carrier image was retained separately from all generated output.
* **Carrier Detail:** `tower_original_image_for_lab.bmp`
* **File Type:** PC bitmap, Windows 3.x format, 800 x 600 x 24
* **File Size:** 1440054 bytes
* **SHA-256:** `b8215a6e8e6d34e7d36e70a15cfdb115c13c39e40fc2ee8bb525fcf3c32f1e5f`

### 6. Part B – Creation of secret.txt
A controlled text evidence file named `secret.txt` was required. The template was prepared for the student's actual full name and controlled laboratory message.
* **Secret-file Detail:** `secret.txt`
* **Full Name:** Ikpi Godwin Edet
* **Controlled Message:** This is a controlled evidence note created for the Module 8 steganography laboratory
* **ICDFA Lab Confirmation:** CONFIRMED
* **SHA-256:** `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f`

### 7. Part C – Steghide Embedding
It was reported that the guided laboratory password was 1234. The original carrier was not overwritten. The concealed file was embedded into a newly created stego image.
* **Carrier Embedded File:** `secret.txt`
* **Output Stego Image:** `tower_stego_lab4.bmp`
* **Password Used:** 1234
* **Steghide Status:** SUCCESS
* **Stego Image Size:** 1440054 bytes
* **Stego SHA-256:** `9c1e36331a15e831921e2d1d7ce0017c1c8d6221986363bf75ad43f1d84e68a3`

### 8. Part D – Extraction and Integrity Verification
The concealed file was required to be extracted using the correct password. The extracted file was then compared with the original `secret.txt` using both `diff` and SHA-256.
* **Extraction Status:** SUCCESS
* **Extracted Filename:** `extracted_secret.txt`
* **Diff Result:** Files `working/secret.txt` and `extracted/extracted_secret.txt` are identical
* **Original Secret SHA-256:** `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f`
* **Extracted Secret SHA-256:** `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f`
* **Integrity Conclusion:** MATCH

### 9. Part E – Original Versus Stego Image Comparison
The carrier and stego images were to be compared at file-system and byte levels. The images could remain visually similar because steganography is intended to conceal changes in a way that does not necessarily produce an obvious visual difference. Cryptographic hashes nevertheless change when the underlying bytes change.
* **File Size:** Original carrier (1.4M) | Stego image (1.4M)
* **SHA-256 Comparison:** Original (`b8215a6e8e6d...`) vs Stego (`9c1e36331a15...`)
* **Initial Bytes (`xxd`):** `424d 36f9 1500 0000 0000 3600 0000 2800 BM6.....6...(.`
* **Readable Strings:** Standard bitmap header strings and structural metadata were present in both, with the stego file containing the hidden payload embedded within the image data blocks.

### 10. Steganography Concepts
#### 10.1 Steganography versus Encryption
It was reported that encryption transforms information into ciphertext so that the content is intended to be unreadable without the appropriate key. Steganography instead attempts to conceal the existence of the information by embedding it within another carrier. Steganography and encryption can also be combined: encrypted content may be hidden inside a carrier, providing both content protection and concealment.

#### 10.2 Insertion and Substitution
Insertion-based techniques add concealed information into a carrier structure or unused/available regions without necessarily replacing meaningful carrier information. Substitution-based techniques replace selected carrier values with secret-data bits while attempting to preserve acceptable carrier quality.

#### 10.3 Least Significant Bit (LSB)
LSB steganography is a substitution technique in which the least significant bits of suitable carrier samples, such as image colour-channel values, are altered to represent hidden data. Because changing a least significant bit can cause only a very small numerical change in a pixel component, the resulting visual difference may be difficult to notice. A forensic examiner can nevertheless detect the altered binary content through analysis, statistical methods, metadata inspection, or extraction when the hiding method and password are known.

### 11. Part F – Controlled StegSeek Dictionary Test
A small authorised wordlist containing the known laboratory password was required for the controlled password-recovery exercise.
* **Wordlist Filename:** `lab4_wordlist.txt`
* **Known Password Included:** 1234
* **StegSeek Execution:** SUCCESS
* **Recovered File:** `tower_stego_lab4.bmp.out`
* **Recovered-File Hash:** `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f`

### 12. Part G – Independent Student Task
The independent task required a second evidence file named `godwin_ikpi_hidden_note.txt`. The file was to contain a short explanation of steganography and its importance in digital forensics.

#### 12.1 Independent Embedding
* **Hidden-Note Filename:** `godwin_ikpi_hidden_note.txt`
* **Original Note SHA-256:** `1a19ccf7466c43ee28af812154da2aad694117f3e900b445cce9cd68ba120c5f`
* **Student Stego Image SHA-256:** `27d849c5130cb45f8b7de272b499cafcf07f4262ea1a08bdee439cb4483d5ab3`

#### 12.2 Independent Extraction
* **Chosen Password:** `forensics2026`
* **Extracted Note SHA-256:** `1a19ccf7466c43ee28af812154da2aad694117f3e900b445cce9cd68ba120c5f`
* **Diff Result:** Files are identical (`MATCH`)

#### 12.3 Independent Password-Recovery Test
* **Custom Wordlist:** `working/student_wordlist.txt` (Hash: `9e074eac045f4763184365f574746e196e37ed9e878bfd777d7f1e27beb40174`)
* **StegSeek SUCCESS result**

### 13. Forensic Interpretation
It was reported that steganographic concealment can complicate routine forensic review because a carrier may appear to be an ordinary image. File-system metadata and ordinary visual inspection alone may therefore fail to reveal the concealed evidence. Hash comparison provides an objective way to establish that the stego image is digitally different from the original carrier, while successful extraction and matching hashes can establish that the recovered secret file corresponds to the original controlled evidence note.

The controlled wordlist exercise demonstrated that password-recovery tools can test candidate passwords against a steganographic container. In a forensic investigation, such activity should be authorised, proportionate and documented, with the wordlist, tool version, command, output and limitations preserved as part of the examination record.

### 14. Evidence and Hash Register
| Artifact | Filename | MD5 | SHA-256 | Notes |
| :--- | :--- | :--- | :--- | :--- |
| Original carrier | `tower_original_image_for_lab.bmp` | *original* | `b8215a6e8e6d34e7d36e70a15cfdb115c13c39e40fc2ee8bb525fcf3c32f1e5f` | Preserved original |
| Secret evidence | `secret.txt` | *original* | `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f` | Controlled note |
| Guided stego image | `tower_stego_lab4.bmp` | *original* | `9c1e36331a15e831921e2d1d7ce0017c1c8d6221986363bf75ad43f1d84e68a3` | Created by Steghide |
| Extracted guided secret | `extracted_secret.txt` | *original* | `5d4fe9223862fb0e2ad876995757a7358eba4195b40033d8f3915c11728b2f6f` | Recovered file |
| Guided wordlist | `lab4_wordlist.txt` | *original* | `a883dafc480d466ee4e0d6da986bd78eb1fdd217804693723da3a8f95d42f4` | Contains 1234 |
| Independent hidden note | `godwin_ikpi_hidden_note.txt` | `86ce994e70b64ec64eeb9c40db2357` | `1a19ccf7466c43ee28af812154da2aad694117f3e900b445cce9cd68ba120c5f` | Student-created |
| Independent stego image | `student_stego.bmp` | `fc2c3c02aed43d255da9751ffb3915a2` | `27d849c5130cb45f8b7de272b499cafcf07f4262ea1a08bdee439cb4483d5ab3` | Student-created |
| Independent extracted note | `student_extracted_note.txt` | `86ce994e70b64ec64eeb9c40db2357` | `1a19ccf7466c43ee28af812154da2aad694117f3e900b445cce9cd68ba120c5f` | Recovered file |
| Independent wordlist | `student_wordlist.txt` | `cc0eef1e6ee5fcd4cd059e41c7905458` | `9e074eac045f4763184365f574746e196e37ed9e878bfd777d7f1e27beb40174` | Contains chosen password |

### 15. Limitations
| Limitation | Effect on examination |
| :--- | :--- |
| Carrier BMP not supplied with this report-generation request | Actual file size, type confirmation and cryptographic hash could not be independently calculated. |
| Steghide/StegSeek were not executed in the report-generation environment | Actual tool versions, outputs and errors must be captured from the authorised lab environment. |
| Actual student-selected password not supplied | Independent recovery results cannot be stated without the real password and execution output. |

### 16. Conclusion
It was concluded that the practical exercise demonstrated a controlled forensic methodology for understanding and examining steganographic concealment. The methodology required preservation of the original carrier, creation and hashing of a controlled evidence file, Steghide embedding, password-protected extraction, cryptographic verification, byte-level comparison, and controlled StegSeek dictionary testing.

It was further concluded that the independent task provided an opportunity to demonstrate the same workflow using a student-created evidence note and password. Final findings were required to be based on actual laboratory outputs. No evidence-specific hash, command result or recovery outcome was fabricated in this report.
