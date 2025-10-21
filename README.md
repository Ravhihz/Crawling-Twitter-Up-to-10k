Crawling and Auto-Resume Pipeline (Colab + Google Drive)

This repository contains a fault-tolerant data-crawling pipeline designed for Google Colab users who need long-running, automatically recoverable processes. The project uses each user’s own authentication token to ensure secure and personalized access. It is capable of continuing execution even when the laptop screen is turned off or the device enters sleep mode, allowing the crawler to operate in a headless environment without interruption.

The system automatically saves progress and resumes from the last checkpoint when a new Colab runtime starts, so users never lose their previous work. Once crawling tasks are complete, the pipeline automatically merges all generated files, ensuring that partial outputs are consolidated into a single, clean dataset. It is also fully integrated with Google Drive, meaning all results, logs, and checkpoints are securely stored and persist across runtime resets.

Users only need to provide their own authentication token in the environment before running the notebook. The pipeline will handle the rest, including saving progress, resuming sessions, and merging results. All sensitive information such as tokens should be kept private and never committed to GitHub. This project is optimized for stability, minimal supervision, and persistent automation.

Please use this project responsibly and ethically. For questions, suggestions, or collaboration inquiries, feel free to contact ravhi.satria@gmail.com
