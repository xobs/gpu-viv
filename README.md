gpu-viv
=======

This contains kernel modules for the various ABIs supported by different Freescale userspace drivers.

Compile the kernel module with:

    make -C {path-to-kernel-directory} M=$PWD AQROOT=$PWD CONFIG_MXC_GPU_VIV=m 

Then copy galcore.ko to your board.


Device Tree
-----------

This module supports device tree configuration.  Add the following entry to your board's .dts file:

        soc {
                gpu {
                        compatible = "fsl,imx6q-gpu";
                        clocks = <&clks 122>, <&clks 74>, <&clks 27>,
                                <&clks 121>, <&clks 26>,
                                <&clks 143>;
                        clock-names = "gpu3d_clk", "gpu3d_shader_clk", "gpu3d_axi_clk",
                                "gpu2d_clk", "gpu2d_axi_clk",
                                "openvg_axi_clk";
                        interrupts = <0 9 0x04>, <0 10 0x04>, <0 11 0x04>;
                        interrupt-names = "irq-3d", "irq-2d", "irq-vg";
                        reg = <0 0>, <0x00130000 0x4000>, <0x00134000 0x4000>, <0x02204000 0x4000>;
                        reg-names = "phys-addr", "iobase-3d", "iobase-2d", "iobase-vg";
                };
        };

Xorg driver
-----------

The xorg driver currently requires a separate DRI module, "Vivante
GC2000:00".  Eventually we'll support imx-drm:00 which is shipping, but for
now you'll have to build the module yourself.


Versions
--------

This has been tested with Linux 3.11.

Each Freescale release has its own branch here.

Note that there are to versions of 4.6.9.6622.  The -old branch is from
L3.0.35_4.0.0_130424 and is compatible with modules from that release.  The
other version is compatible with the latest BSP, available from git.
