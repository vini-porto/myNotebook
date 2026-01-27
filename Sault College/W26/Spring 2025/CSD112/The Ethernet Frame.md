When computers send data, they wrap it in an Ethernet frame. Think of it like addressing an envelope with extra security features.

1. Preamble (7 bytes)
	- Gets everyone's attention and syncs up the timing.
2. Start Frame Delimiter (1 byte)
	- Where the real content begins
3. Destination Address (6 bytes)
4. Source Address (6 bytes)
5. Type/Length Field (2 bytes)
	- Either tells you what kind of data this is (like IPv4) OR how big the data is.
6. Data (46-1500 bytes)
7. Frame Check Sequence (4 bytes)