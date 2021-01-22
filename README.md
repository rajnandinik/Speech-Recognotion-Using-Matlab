# Speech-Recognotion-Using-Matlab code
clc;
clear all;
close all;
%input an audio(mp3) signal
[z,Fs2] = audioread('E:\audioclipsfordspcolours\blue--_gb_1.mp3');
%play the input audio file
sound(z,Fs2);

%psd of audio signal
periodogram(z);

%mean of the psd
mean_blue=mean(periodogram(z));
disp("Mean of blue="+mean_blue);

%median of psd
median_blue=median(periodogram(z));
disp("Median of blue= "+median_blue);

%max peak of psd
pks_blue=findpeaks(periodogram(z));
max_blue=max(pks_blue);
disp("peak of blue = "+max_blue);
T=readtable('E:\audioclipsfordspcolours\colours.xlsx');


%creating table for testing the sample input
header={'mean','median','peak'};
xlswrite('E:\audioclipsfordspcolours\t.xlsx',header);
info={mean_blue,median_blue,max_blue};
xlswrite('E:\audioclipsfordspcolours\t.xlsx',info,'Sheet1','A2');

test=readtable('E:\audioclipsfordspcolours\t.xlsx');
for i=1:10
if test{1,1}==T{i,2}&&test{1,2}==T{i,3}&&test{1,3}==T{i,4}%compares the Mean median and max power of the signal with database
    disp(T(i,1)); %displays name of the colour
 %displays the index of colour

end
end
