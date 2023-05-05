Download Link: https://assignmentchef.com/product/solved-ece3780-lab3-investigating-the-fourier-series-filtering
<br>
The following Matlab function (see below) plots the Fourier synthesis of the function <em>f</em>(<em>t</em>) = <em>t</em> for -π &lt; <em>t </em>&lt; π.  That is

<ol>

 <li>Calculate mathematically the Fourier coefficients and verify that the expression between the <em>for loop </em>is correct.</li>

 <li>Why are there only Sine terms? Why there is no DC value?</li>

 <li>Calculate the Fourier series for <em>f</em>(<em>t</em>) = <em>A</em>+ <em>t</em> for -π &lt; <em>t</em> &lt; π, where <em>A</em> is a constant. What are the differences in the coefficients compared to part a)? Plot these coefficients for both cases so that you can see the differences and similarities.</li>

 <li>Modify the program and plot this new series that you obtained in part c)</li>

 <li>Plot and Calculate the Fourier coefficients for <em>f</em>(<em>t</em>) = <em>t</em> Cos(<em>t</em>/2) for -π &lt; <em>t</em> &lt; π. Plot <em>f</em>(<em>t</em>).</li>

 <li>Do the coefficients in e) have higher amplitude than in a)? Write an explanation of these differences. Hint, remember that the signal <em>f</em>(<em>t</em>) is not periodic but you are assuming periodicity and your series approximation is only valid for -π &lt; <em>t</em> &lt; π. Therefore, regardless of <em>f</em>(<em>t</em>), this signal repeats itself every 2 π.</li>

</ol>

function fourser(N);




% N = number of coefficients to be used (input)

% Plot the Fourier series for f(t) = t for -pi&lt;t&lt;pi




t = -pi:pi/200:pi;




fsm = zeros(N-1,length(t));




for i = 1:(N-1)    cn = 2*((-1)^(i+1))/i;     fsm(i,:) = cn*sin(i*t);

end




fsm2 = sum(fsm);




plot(t,t,t,fsm2)  title([‘Fourier Series’, ‘ N = ‘, num2str(N)]) xlabel(‘Time’), ylabel(‘Amplitude’)  legend(‘Function f(t)’, ‘Fourier series approx’)  <strong><u>Part II</u>  </strong>

<strong> </strong>

As you see in Table 6.1, to calculate the different versions of the Fourier series of a periodic signal requires a number of integrals.

Matlab provides functions for solving, plotting, and manipulating symbolic math equations. You can analytically perform differentiation, integration, simplification, transforms, and equation solving.

In order to illustrate this, we will solve Example 6.1 shown in the figure below.

First, create the symbolic variables <em>t</em>,

syms t

Then assign the expression to <em>x</em>:




x = exp(-0.5*t)




Need the expressions now for the Fourier series coeffcients.




First, for the value π notice the difference in Matlab. Type and execute the following in the Comand window

&gt;&gt; sin(sym(pi))

&gt;&gt; sin(pi)




What values do you have for both operations?




Continuing with the coefficients and calculating the Trigonometric ones




syms n




Start with <em>a</em><sub>o</sub> and do the integral




&gt;&gt; ao = int((1/pi)*x, 0 , pi)




Evaluate your result




&gt;&gt; ao_coeff = eval(ao)




Continue with <em>a<sub>n</sub></em>




&gt;&gt; an = int(((2/pi)*x*sym(cos(2*n*t))),t, 0,pi)




If you want to see the first 10 <em>a<sub>n</sub></em> and <em>b<sub>n</sub></em> coefficients for n = 1: 10 do the following




&gt;&gt; n=1:10;

&gt;&gt; an_coeffs= eval(an)

&gt;&gt; bn = int(((2/pi)*x*sym(sin(2*n*t))),t, 0,pi)

&gt;&gt; bn_coeffs = eval(bn)




Those are for the Trigonometric. The compact trigonometric as calculated in your textbook are:




&gt;&gt; cn = sqrt(an_coeffs.^2 + bn_coeffs.^2)

&gt;&gt; subplot(211)

&gt;&gt; inde = 0:10;

&gt;&gt; stem(inde,[ao_coeff cn])

&gt;&gt; title(‘Example 6.1’)

&gt;&gt; xlabel(‘Index (multiple of fundamental frequency)’)

&gt;&gt; ylabel(‘cn’)

&gt;&gt; subplot(212)

&gt;&gt; angles = atan(-bn_coeffs./an_coeffs)

&gt;&gt; stem(inde,[0 angles])

&gt;&gt; title(‘Phase’)

&gt;&gt; xlabel(‘Index (multiple of fundamental frequency)’)

&gt;&gt; ylabel(‘degrees, radian’)







Please do the same for the signal in Example 6.2 shown in the next figure.










Repeat Example 6.2 when <em>x</em>(<em>t</em>) is <em>x</em>(<em>t</em>-0.5) and <em>x</em>(<em>t</em>+0.5). Comment on the symmetry of the original 6.2 problem and the new time shifted versions and the coefficients you obtained.




<strong><u>Part III</u>  </strong>

Create a signal sequence of length 200 that its first 13 samples are:

x(1:13)=[1 1 1 1 -1 -1 1 1 -1 1 -1 1];  x(14:200)=0;

Then, create a Gaussian random sequence (use the command “randn” in MATLAB) with zero mean and a variance that is being determined by the Signal to Noise Ratio (SNR). Now, write a simple script that generates the output of the following system.




Furthermore, calculate the crosscorrelation of the output of the above system and the original signal and plot it.




Calculate the variance of the random signals for the SNR values of 10, 5, 1 and 0.1 and observe the results. What can you say about correlations and detection of signals buried in noise?




<strong>Handout:  </strong>

<ol>

 <li>Plot of the original signal and the output signal (use subplot to save paper!).</li>

 <li>Plot of the crosscorrelation of the y(n) and x(n) for only 50 samples chosen from the middle of <em>r<sub>xy</sub>(n)</em> at different SNR values and the estimated delay of the system from the crosscorrlation function.</li>

</ol>

.




<strong>Part IV</strong>




Ask the TA for the file seashell.wav. (you can pick any other wave files that are in the windows directory of your lab computer.) You can load this file to MATLAB by the

command: [x, fs]=wavread(‘seashell’);

And then you can play it by command: <sub>soundsc(x,fs) </sub>




To see what filtering convolution with a simple impulse response looks like try the following:

<h1>soundsc(conv(x,[1 -1]),fs);  and soundsc(conv(x,[1 1 1 1 1 1 1]),fs);</h1>







What difference do you hear? Are they making the sound lower in pitch or higher? You may try different length for <em>h</em>(<em>t</em>) and see its effect.


