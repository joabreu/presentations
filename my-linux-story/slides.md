---
theme: ../slidev-theme-joabreu
layout: cover
title: My Linux Story
---

# My Linux Story

## OSS Contributions

`Signed-off-by: Jose Abreu <joabreu at synopsys.com>`

---

# The Start

<Window title="Add I2S/ADV7511 audio support for ARC AXS10x boards">
```text{all|18}
From:       Jose.Abreu () synopsys ! com (Jose Abreu)
Date:       2016-03-28 9:41:48

ARC AXS10x platforms consist of a mainboard with several peripherals.
One of those peripherals is an HDMI output port controlled by ADV7511 transmitter.

This patch set adds audio for the ADV7511 transmitter and I2S audio for the
AXS10x platform.

Jose Abreu (4):
  drm/i2c/adv7511: Add audio support
  ARC: axs10x: Update defconfigs so that audio is enabled
  ASoC: dwc: Add I2S HDMI audio support using custom platform driver
  ARC: axs10x: Update defconfigs so that I2S is enabled

...

13 files changed, 1771 insertions(+), 1041 deletions(-)
```
</Window>

---

# The Response

<Window title="Re: [PATCH 2/3 v2] ASoC: dwc: Add I2S HDMI audio support">
```text{6}
>  sound/soc/dwc/Kconfig          |   1 +
>  sound/soc/dwc/designware_i2s.c | 385 +++++++++++++++++++++++++++++++++++++++--

Your changelog appears to describe the writing of a machine driver but
this is a large patch adding code to an I2S controller driver.  This means
I can't review your patch since I can't tell what it is supposed to do.

...
```
</Window>

#### My Clarification

<Window title="Re: [PATCH 2/3 v2] ASoC: dwc: Add I2S HDMI audio support">
```text{5,6,7}
I can separate the platform driver into a new file but they will have to be
compiled into the same module as the new additions to the i2s driver depend on
functions of the platform driver (see i2s_irq_handler()). Or should I divide
this into two modules and add a Kconfig option to the platform driver?
Besides this I first wanted the driver to be compiled into the same module so
that it is compatible with kernel 3.18 where simple audio card requires that
platform driver == cpu driver.
```
</Window>

---

# My First Mistake

<Window title="Re: [PATCH 2/3 v2] ASoC: dwc: Add I2S HDMI audio support">
```text{4,5,9,10,11}
No, that's not at all acceptable. The Designware IP is not specific to
your system, you can't make it depend on your platform driver. The kernel
needs to work on other people's systems too.
You need to work through and/or extend the abstractions the framework
provides to separate the drivers for different IPs.

...

That's not OK upstream, we're working on the current kernel not on
random old kernels.  We don't carry compatibility code to enable current
kernel code to be run on years old kernels.
```
</Window>

---
layout: fact
---

# Lesson One
*Always develop and test your code against the mainline tree of the affected subsystem*