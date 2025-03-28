---
layout: post
title: Block Cipher Modes
---

For a general analysis of various Block Cipher Modes checkout the excellent report by Rogaway [Evaluation of some Blockcipher Modes of Operation](https://www.cryptrec.go.jp/exreport/cryptrec-ex-2012-2010r1.pdf)

# ECB Mode

<div style="text-align: center">
{% include_relative ecb.tikz.md %}
</div>


Defined In: *Common Knowledge????*

Not used at all!!


# CBC Mode

Defined In: [NIST SP-800-38A](http://csrc.nist.gov)
<div style="text-align: center">

{% include_relative cbc.tikz.md %}
</div>

# CFB Mode

Defined In: [NIST SP-800-38A](http://csrc.nist.gov)
<div style="text-align: center">

{% include_relative cfb.tikz.md %}
</div>
