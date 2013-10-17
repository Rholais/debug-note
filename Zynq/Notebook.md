Notebook for Zynq
=================

2013.10.17
----------
`ps7_gpio_0` was found in dts made by SDK.

	ps7_gpio_0: ps7-gpio@e000a000 {
		#gpio-cells = <2>;
		compatible = "xlnx,ps7-gpio-1.00.a";
		emio-gpio-width = <64>;
		gpio-controller ;
		gpio-mask-high = <0x3c000>;
		gpio-mask-low = <0x0>;
		interrupt-parent = <&ps7_scugic_0>;
		interrupts = < 0 20 4 >;
		reg = < 0xe000a000 0x1000 >;
	} ;

This was used to build the block of `ad9516_3` in dts.

	ad9516_3 {
		compatible = "xjtu,ad9516-gpio";
		/* SPI-GPIOs */
		spi-bus-num = <2>;
		spi-speed-hz = <4000000>;
		spi-mosi-gpio = <&ps7_gpio_0 46 0>;
		spi-miso-gpio = <&ps7_gpio_0 47 0>;
		spi-clk-gpio = <&ps7_gpio_0 48 0>;
		spi-cs-gpio = <&ps7_gpio_0 49 0>;
	};
