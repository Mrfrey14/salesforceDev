Install/Setup guide for Jest:

1) Download nodejs here: [Node JS Install](https://nodejs.org/en/download/) or use chocolately and nodist if you know what you're doing (this approach is a bit better imo): [NodeJS Nodist Install Instructions](https://github.com/nullivex/nodist)

2) Install Jest CLI via the CLI using the command: npm install -g jest-cli (or npm install --save-dev jest-cli for a local project install)

3) You may need to change your execution policy since jest doesn't register as a known Windows Package currently. Open powershell as an admin and enter the following command: Set-ExecutionPolicy Unrestricted
    a) When prompted, type the value A and then hit enter

