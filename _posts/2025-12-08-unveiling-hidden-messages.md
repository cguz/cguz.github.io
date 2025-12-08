---
title: "Detect leaking data"
date: 2025-12-08
categories: [security, steganography, AI]
tags: [forensics, homoglyphs, python]
excerpt: "Discover the steganographic techniques used to hide data within PDF documents using homoglyphs, and the algorithmic approach to retrieve them."
---

In this post, we explore the algorithmic approach used to retrieve the hidden flags for files 1 and 2 of the [hackathon](https://atpi.eventsair.com/ai-star-2025/hackathon) organized by KP Labs, Centre for Credible AI and European Space Agency in the [AI STAR 2025 conference](https://atpi.eventsair.com/ai-star-2025/).

## Homoglyph Steganography

This involves replacing specific characters in a text with "homoglyphs" — characters that look identical (or very similar) to the original but have different Unicode values.

The files contain a mix of two different characters (e.g., a standard Latin 'a' and a Cyrillic 'а'). 

By assigning a binary value (0 or 1) to each variant, a hidden binary stream can be embedded directly into the document's text.

## The 'o' Anomaly

Upon analyzing the text extracted from `1.pdf`, we observed an anomaly in the character 'o'. While most instances were the standard Latin 'o' (`U+006F`), some were actually the character 'ö' (o-umlaut, `U+00F6`), likely stripped of its dots or rendered in a font where the difference is imperceptible.

**Solution:**

```
1.  Scan the text for every occurrence of 'o' and 'ö'.
2.  Perform a binary Conversion:
    - Latin 'o' -> `0`
    - Umlaut 'ö' -> `1`
3.  The generated binary stream, when grouped into 8-bit bytes and converted to ASCII, the hidden flag is revealed.
```

## The Interleaved 'a'

File 2 presented a more subtle challenge. 

The target character was 'a'. The text contained a mix of the standard Latin 'a' (`U+0061`) and the Cyrillic small letter 'а' (`U+0430`). Visually, they are identical in most fonts.

Simply converting these characters to binary (Latin 'a' -> 0, Cyrillic 'а' -> 1) did not immediately yield a readable message. The resulting binary stream appeared corrupted.

**Solution:**

```
1. Isolate all 'a' and 'а' characters.
2. Map Latin 'a' to `0` and Cyrillic 'а' to `1`.
3. Place the message bits at every second position (indices 0, 2, 4...), effectively interleaving the real data with "noise" bits (or zeros).
4. After extracting every second bit, the resulting stream decoded perfectly into the hidden English sentence.
```

As we can see in step 3 of the algorithm, the solution required applying a stride of 2.

For the full solution and code, check out the repository: [Detect Leaking Data: Safeguarding AI for Space](https://github.com/Hackatoon/Detect-Leaking-Data-Safeguarding-AI-for-Space).
