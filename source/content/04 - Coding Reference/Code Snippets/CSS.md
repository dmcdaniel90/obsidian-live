>[!code] Adding a background banner to a heading
>```css
>h1 {
>	position: relative;
>	z-index: 1;
>}
>h1::before {
>	content: '';
>	position: absolute;
>	top: 50%;
>	left: 0;
>	width: 100%;
>	height: 40%;
>	background-color: hsl(228, 96%, 89%);
>	transform: translateY(-50%) rotate(-3deg);
>	z-index: -1;
>}
