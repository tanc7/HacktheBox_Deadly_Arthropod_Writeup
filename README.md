This was a really fun exercise and a lesson to be taught, that USB keyboard keystrokes can be captured as a pcap file.

Originally, I was stumped, and looked online to find this ![original_keymappper](https://medium.com/@ali.bawazeeer/kaizen-ctf-2018-reverse-engineer-usb-keystrok-from-pcap-file-2412351679f4)

The original keystroke mapper was pretty shoddy and did not consider CAPITALIZED characters. A better solution I found here  ![better solution](https://bitvijays.github.io/LFC-Forensics.html)

# Solution

First use tshark to strip out only the keyscans

<code>tshark -r deadly_arthropod.pcap -T fields -e usb.capdata > keystrokes.txt</code>

When you program the script and run it the first time, make sure you clear out empty whitespaces from the capture file with the <code>cat keystrokes.txt | awk 'NF' > pipe;cat pipe > keystrokes.txt</code> command. Otherwise the script will throw an error as it does not interpret empty lines.

Originally I received two faux keys and one final string of gibberish that I did not understand.

<code>eks@hackthebox.eu
Th1sC0uldB3MyR3alP@ssw0rd
QK<_>.<<<<H>5<<{_<I>>ck>'>>b0<<<<<<<<<I<<<<T>>f>>>>>>_>>>>>>}<.<.<<<<3<<<<<<<<u<<t_>>a<<<<<<<<<<B>>>>>>>>>>>>>>t>5<<<I>>>_>>>>>a<<<<<<a>>>>>>d<<<<y>>>r
</code>

You're not done yet. On line #3, follow the keystrokes, '<' is left arrow, and '>' is right arrow. If you did it correctly, you will find the key as:

<code>
HTB{If_It_Quack5_It'5_a_K3yb0ard...}
</code>

Submit it and get your points!

# Conclusion

This was a very fun exercise and I enjoyed it, particularly how pcap file formats can be used to capture keystrokes as well.
