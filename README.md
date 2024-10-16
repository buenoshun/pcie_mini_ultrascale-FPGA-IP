# pcie_mini_ultrascale-FPGA-IP
An VHDL FPGA IP core to implement transaction layer logic for Xilinx Ultrascale PCIe hard-IP

To download: Click the zip file, on the next page click "view raw" to download it.

originally hosted (in 2019) at: 
https://opencores.org/projects/pcie_mini_axi4s_wb
Since the OpenCores.org admins have abandoned their website, and don't allow new users to register and download old projects (like this one), I, Istvan Nagy, the sole author, decided to re-release the project on GitHub. The new release is with a new, less restrictive license: "BSD zero clause", instead of the old LGPL. This will allow companies to use it in their product without restrictions or obligations.
The BSD 0-clause license: Copyright (C) 2024 by Istvan Nagy buenoshun@gmail.com 
Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted. THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE.

UN-TESTED !

Created by Istvan Nagy This IP core creates a PCI-express to Wishbone bridge for Xilinx Kintex Ultrascale+ FPGAs. It is based on a core I made for the Xilinx Spartan-6 FPGAs, the "pcie_mini". https://opencores.org/projects/pcie_mini It is called "mini" because it is few lines of code, nothing to do with mini-pci form factor. The original SP6 pcie_mini was tested and debugged on various boards, and was working fine. I is ideal for low performance peripheral functions using Wishbone bus interconnect and using OpenCores peripheral IP cores. The PCI-express endpoint block code that is generated by the Xilinx Vivado tools have lots of ports and have an AXI4-Streaming interface, with partially decoded-recoded TLP packet headers, not with real address/data-based bus. This core encapsulates the Xilinx core and makes it to have Wishbone bus at the top level.

!!NEED VOLUNTEERS!!! This new PCIe_mini_axi4s_wb core v1.0 was fully written, synthesized and implemented (passes P&R), but was never tested or debugged on any target platform, as of October 2019. So probably it DOES NOT WORK yet. Therefore I NEED VOLUNTEERS for on-target debugging and finishing up the project. Possible locations for bugs, the parts that changed from the original SP6 version, the TLP (axi4s descriptor) bit field decoding, the 32-to-64bit fifo dword ordering, the axi4s-to-TRN conversion, the hundreds of control ports of the new IP, the clocking... If you have made it work in your lab, please contact me at buenos -AT- freemail.hu, and we can release your files.

Some other info about how it works and how to use it, can be found in the header section of the attached source files. example_device_top.vhd --> This file is just for demonstration and test compilation. pcie_mini_axi4s_wb.vhd --> This file is the core top level file that you instantiate into your own project. pcie_axi4s2trn_wrapper.vhd --> This file is a sub module, for handling all the hundreds of ports of the xilinx IP-catalog-generated core, and it also converts the AXI4-stream bus into a TRN bus that works with the original pcie_mini IP (after some modifications on it too).

Environment: Xilinx Vivado 2019.1 implementation tools. Target device: Kintex Ultrascale+ XCKU3P-1FFVA676-3-E or similar. Utilization: 2% (LOL!).
