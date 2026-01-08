# Lab
Ex08

Ex.No: 8	Study of TCP/UDP performance using Simulation tool. AIM:
To simulate the performance of TCP/UDP using NS2.


TCP Performance 
Algorithm

Create a Simulator object.
Set routing as dynamic.
Open the trace and nam trace files.
Define the finish procedure.
Create nodes and the links between them.
Create the agents and attach them to the nodes.
Create the applications and attach them to the tcp agent.

Connect tcp and tcp sink.
Run the simulation.


PROGRAM:

set ns [new Simulator]
$ns color 0 Blue
$ns color 1 Red
$ns color 2 Yellow set n0 [$ns node] set n1 [$ns node] set n2 [$ns node] set n3 [$ns node]
set f [open tcpout.tr w]
$ns trace-all $f
set nf [open tcpout.nam w]
$ns namtrace-all $nf
$ns duplex-link $n0 $n2 5Mb 2ms DropTail
$ns duplex-link $n1 $n2 5Mb 2ms DropTail
$ns duplex-link $n2 $n3 1.5Mb 10ms DropTail
$ns duplex-link-op $n0 $n2 orient right-up
$ns duplex-link-op $n1 $n2 orient right-down
$ns duplex-link-op $n2 $n3 orient right
$ns duplex-link-op $n2 $n3 queuePos 0.5 set tcp [new Agent/TCP]
$tcp set class_ 1
set sink [new Agent/TCPSink]
$ns attach-agent $n1 $tcp
$ns attach-agent $n3 $sink
$ns connect $tcp $sink
set ftp [new Application/FTP]
$ftp attach-agent $tcp
$ns at 1.2 "$ftp start"
$ns at 1.35 "$ns detach-agent $n1 $tcp ; $ns detach-agent $n3 $sink"
$ns at 3.0 "finish" proc finish {} {
global ns f nf











}
$ns run


Output
$ns flush-trace close $f
close $nf
puts "Running nam.."
exec xgraph tcpout.tr -geometry 600x800 & exec nam tcpout.nam &
exit 0




UDP Performance
ALGORITHM :
Create a Simulator object.
Set routing as dynamic.
Open the trace and nam trace files.
Define the finish procedure.
Create nodes and the links between them.
Create the agents and attach them to the nodes.
Create the applications and attach them to the UDP agent.
Connect udp and null agents.
Run the simulation.

PROGRAM:
set ns [new Simulator]
$ns color 0 Blue
$ns color 1 Red
$ns color 2 Yellow set n0 [$ns node] set n1 [$ns node] set n2 [$ns node] set n3 [$ns node]
set f [open udpout.tr w]
$ns trace-all $f
set nf [open udpout.nam w]
$ns namtrace-all $nf
$ns duplex-link $n0 $n2 5Mb 2ms DropTail
$ns duplex-link $n1 $n2 5Mb 2ms DropTail
$ns duplex-link $n2 $n3 1.5Mb 10ms DropTail
$ns duplex-link-op $n0 $n2 orient right-up
$ns duplex-link-op $n1 $n2 orient right-down
$ns duplex-link-op $n2 $n3 orient right
$ns duplex-link-op $n2 $n3 queuePos 0.5 set udp0 [new Agent/UDP]
$ns attach-agent $n0 $udp0
set cbr0 [new Application/Traffic/CBR]
$cbr0 attach-agent $udp0 set udp1 [new Agent/UDP]
$ns attach-agent $n3 $udp1

$udp1 set class_ 0
set cbr1 [new Application/Traffic/CBR]
$cbr1 attach-agent $udp1 set null0 [new Agent/Null]
$ns attach-agent $n1 $null0 set null1 [new Agent/Null]
$ns attach-agent $n1 $null1
$ns connect $udp0 $null0
$ns connect $udp1 $null1
$ns at 1.0 "$cbr0 start"
$ns at 1.1 "$cbr1 start"
puts [$cbr0 set packetSize_] puts [$cbr0 set interval_]
$ns at 3.0 "finish" proc finish {} {
global ns f nf
$ns flush-trace close $f
close $nf
puts "Running nam.." exec nam udpout.nam & exit 0
}
$ns run


Output:








VIVA (Pre & Post)Lab Questions
How is a TCP connection closed?
What is Flow control in TCP?
What protocol is TCP?
How is TCP Reliable?
What is TCP?
Explain the three way Handshake process?
What are the 6 TCP flags?
Explain how TCP avoids a network meltdown?







RESULT :
Thus the study of TCP/UDP performance is done successfully.
