
---

## Introduction

Offline **open-source personal assistant** who can live **on your server**.

That **does stuff** when you **ask it to**.

You can **talk to him** and he can **talk to you**.
You can also **text hi** and he can also **reply you**.
If you want to, It can communicate with you by being **offline to protect your privacy**.

### Why?

> 1. If you are a developer (or not), you may want to build many things that could help in your daily life.
> Instead of building a dedicated project for each of those ideas, Leon can help you with his
> packages/modules (skills) structure.
> 2. With this generic structure, everyone can create their own modules and share them with others.
> Therefore there is only one core (to rule them all).
> 3. Leon uses AI concepts, which is cool.
> 4. Privacy matters, you can configure Leon to talk with him offline. You can already text with him without any third party services.
> 5. Open source is great.

### What is this repository for?

> This repository contains the following nodes of Leon:
> - The server
> - The packages/modules
> - The web app
> - The hotword node

### What is Leon able to do?

> Today, the most interesting part is about his core and the way he can scale up. He is pretty young but can easily scale to have new features (packages/modules).


Sounds good for you? Then let's get started!

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 10 or 11
- npm >= 5
- [Python](https://www.python.org/downloads/) >= 3
- [Pipenv](https://docs.pipenv.org)
- Supported OSes: Linux, macOS and Windows



### Installation

```sh
# Clone the repository (stable branch)
git clone https://github.com/nhadiq97/AIROBOT


# Go to the project root
cd AIROBOT/LEON

# Install
npm install
```

### Usage

```sh
# Check the setup went well
npm run check

# Build
npm run build

# Run
npm start

# Go to http://localhost:1337
# Hooray! Leon is running
```

### Docker Installation

```sh
# Build
npm run docker:build

# Run on Linux or macOS
npm run docker:run

# Run on Windows (you can replace "UTC" by your time zone)
docker run -e TZ=UTC -p 1337:1337 -it leonai/leon

# Go to http://localhost:1337
# Hooray! Leon is running
```




