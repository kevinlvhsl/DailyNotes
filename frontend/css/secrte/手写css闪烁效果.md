 ##  闪烁效果
 
 > css

 /**
 * Blinking
 */
 ```
@keyframes blink-1 { 50% { color: transparent } }
@keyframes blink-2 { to { color: transparent } }

p {
	padding: 1em;
	background: gold;
}

.blink-smooth-1 {
	animation: 1s blink-1 infinite;
}

.blink-smooth-2 {
	animation: .5s blink-2 6;
	animation-direction: alternate;}

.blink {
	animation: 1s blink-1 3 steps(1);
}
 ```
 
> HTML
```
<p class="blink-smooth-1">Peek-a-boo!111111</p>
<p class="blink-smooth-2">Peek-a-boo!2222</p>
<p class="blink">Peek-a-boo!3333</p>
```

 [http://play.csssecrets.io/blink](http://play.csssecrets.io/blink)
