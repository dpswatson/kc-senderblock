# kc-senderblock
A Bash script for Kerio Connect servers to filter senders from messages that users have marked as spam.

This script addresses what many users perceive as a deficiency in Kerio Connect: Even after they've marked messages as spam, there is still a very good chance that they will receive new messages from the same sender. KC actually uses the cumulative spam/not spam desgnations to train the Beyesian filter built into SpamAssassin, but does not set a block on the sender. If a message with the same sender and recipient is received again, there is a good chance that the server will still not recognize it as spam.

The script is designed to work in conjunction with a swatch process that is monitoring the spam.log file on the KC server. If a line is added to the file that indicates that a user has marked a message as either spam or not spam, or has manually moved a message into the Junk E-mail folder, that line to piped to the script, which then processes it and takes appropriate action. If a message is marked as spam or moved into the Junk E-mail folder, a filter rule is created (or modified if it already exists) to move new messages from the sender to the Junk E-mail folder automotically. If a message is marked as not spam, the sender is removed from the list (if present). 

I wrote this script for my own use, and have only tested it on Ubuntu Linux thus far. I suspect it will run properly on any Linux distro. It may require some modifications to run on a Mac. On Windows, you may be able to get it working with Cygwin (https://www.cygwin.com/).

The script was designed to run on the KC server itself, but it should run fine on another machine as long as it has full read/write access to the mail store directory. All editions of KC use the same structure within the store directory, so it should be compatible with any edition. If you have multiple KC servers, you will need to configure a separate swatch and script instance for each server.

