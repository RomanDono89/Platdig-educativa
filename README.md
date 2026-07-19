# Platdig-educativa

A CLI tool for accessing my university's web platform.

## Installation

Install the required dependencies:

```bash
curl, iconv (usually provided by glibc on most distributions), wget, python3, GNU coreutils, etc.
```

Clone the repository:

```bash
cd /tmp
git clone https://github.com/RomanDono89/Platdig-educativa.git
```

Enter the project directory:

```bash
cd Platdig-educativa
```

Install the CLI tool:

```bash
sudo install educativa /usr/local/bin/educativa
```

## Usage

Run the command:

```bash
educativa
```

## Automatic Login

If you don't want to enter your credentials every time, edit the script and replace:

```sh
# enter user
printf "enter your user: "
read user

# enter password without echoing it to the terminal
printf "enter your password: "
trap 'stty echo; printf "\n"; exit' INT TERM EXIT
stty -echo
read -r pass
stty echo
trap - INT TERM EXIT
printf "\n"

# hash password
pass=$(printf "%s" "$pass" | md5sum - | cut -d " " -f1)
```

with:

```sh
user="your_dni"
pass="$(printf "%s" "your_password" | md5sum - | cut -d " " -f1)"
```

Alternatively, you can pre-compute the hash once:

```sh
printf "%s" "your_password" | md5sum - | cut -d " " -f1
```

and store only the resulting hash in the script:

```sh
user="your_dni"
pass="your_precomputed_md5_hash"
```

This avoids storing your password in plain text (although the MD5 hash itself should still be treated as sensitive, since it can be used to authenticate).

## To Do

- Add support for "Presentación".
- Remove the Python dependency.
- Refactor the code.

Pull requests and suggestions are welcome.
