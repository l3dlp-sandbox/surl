[![Go Report Card](https://goreportcard.com/badge/github.com/leg100/signer)](https://goreportcard.com/report/github.com/leg100/signer)
[![Version](https://img.shields.io/badge/goversion-1.18.x-blue.svg)](https://golang.org)
[![License](http://img.shields.io/badge/license-mit-blue.svg?style=flat-square)](https://raw.githubusercontent.com/leg100/goblender/master/LICENSE)
![Tests](https://github.com/leg100/signer/actions/workflows/tests.yml/badge.svg)
# Signer

Signer creates signed URLs that expire after a given time.

## Installation

`go get github.com/leg100/signer@latest`

## Usage

```golang

package main

import (
	"fmt"
	"time"

	"github.com/leg100/signer"
)

func main() {
	sign := signer.New([]byte("secret_sesame"))

	signed, _ := sign.SignURL("https://example.com/a/b/c?foo=bar", time.Hour)

	fmt.Println("signed url:", signed)

	// Outputs something like:
	//
	// https://example.com/signed/pTn2am3eh8Ndz7ZTb6ya2gOMA5XtnFRd-1M__TNQr9o.1664441797/a/b/c?foo

	err := sign.VerifyURL(signed)
	if err != nil {
		fmt.Println("verification failed:", err.Error())
	}
	fmt.Println("verification succeeded")
}

```
