
# FPGA settings
FPGA_TOP = fpga
FPGA_FAMILY = "Stratix V"
FPGA_DEVICE = 5SGXEA7N2F45C2

# Files for synthesis
SYN_FILES = rtl/fpga.v
SYN_FILES += rtl/fpga_core.v
SYN_FILES += rtl/debounce_switch.v
SYN_FILES += rtl/sync_reset.v
SYN_FILES += rtl/sync_signal.v
SYN_FILES += rtl/i2c_master.v
SYN_FILES += rtl/si570_i2c_init.v
SYN_FILES += lib/eth/rtl/eth_mac_10g_fifo.v
SYN_FILES += lib/eth/rtl/eth_mac_10g.v
SYN_FILES += lib/eth/rtl/eth_mac_10g_rx.v
SYN_FILES += lib/eth/rtl/eth_mac_10g_tx.v
SYN_FILES += lib/eth/rtl/lfsr.v
SYN_FILES += lib/eth/rtl/eth_axis_rx_64.v
SYN_FILES += lib/eth/rtl/eth_axis_tx_64.v
SYN_FILES += lib/eth/rtl/udp_complete_64.v
SYN_FILES += lib/eth/rtl/udp_checksum_gen_64.v
SYN_FILES += lib/eth/rtl/udp_64.v
SYN_FILES += lib/eth/rtl/udp_ip_rx_64.v
SYN_FILES += lib/eth/rtl/udp_ip_tx_64.v
SYN_FILES += lib/eth/rtl/ip_complete_64.v
SYN_FILES += lib/eth/rtl/ip_64.v
SYN_FILES += lib/eth/rtl/ip_eth_rx_64.v
SYN_FILES += lib/eth/rtl/ip_eth_tx_64.v
SYN_FILES += lib/eth/rtl/ip_arb_mux_64_2.v
SYN_FILES += lib/eth/rtl/ip_mux_64_2.v
SYN_FILES += lib/eth/rtl/arp_64.v
SYN_FILES += lib/eth/rtl/arp_cache.v
SYN_FILES += lib/eth/rtl/arp_eth_rx_64.v
SYN_FILES += lib/eth/rtl/arp_eth_tx_64.v
SYN_FILES += lib/eth/rtl/eth_arb_mux_64_2.v
SYN_FILES += lib/eth/rtl/eth_mux_64_2.v
SYN_FILES += lib/eth/rtl/xgmii_interleave.v
SYN_FILES += lib/eth/rtl/xgmii_deinterleave.v
SYN_FILES += lib/eth/lib/axis/rtl/arbiter.v
SYN_FILES += lib/eth/lib/axis/rtl/priority_encoder.v
SYN_FILES += lib/eth/lib/axis/rtl/axis_fifo.v
SYN_FILES += lib/eth/lib/axis/rtl/axis_async_frame_fifo.v
SYN_FILES += cores/phy/phy.qip
SYN_FILES += cores/phy_reconfig/phy_reconfig.qip

# QSF files
QSF_FILES = fpga.qsf

# SDC files
SDC_FILES = fpga.sdc

include ../common/altera.mk

program: fpga
	quartus_pgm --no_banner --mode=jtag -o "P;$(FPGA_TOP).sof"

# program with 'factory default' parallel flash loader design (or something else with a NIOS2 that can see the flash chips)
program_flash_pfl: fpga
	nios2_command_shell.sh sof2flash --input="$(FPGA_TOP).sof" --output="$(FPGA_TOP).flash" --offset=0x20C0000 --pfl --optionbit=0x00030000 --programmingmode=PS
	nios2_command_shell.sh nios2-flash-programmer --base=0x0 "$(FPGA_TOP).flash"
