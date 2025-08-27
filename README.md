## Is This Point on the Line?

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Is This Point on the Line?</title>
	<style>
		body { font-family: Arial, sans-serif; }
		#solution { padding: 20px; margin-top: 10px; display: none; }
		#graph { width: 300px; height: 200px; border: 1px solid #ccc; background: #fff; }
		.expander { cursor: pointer; color: #0077cc; text-decoration: underline; }
	</style>
</head>
<body>
	<h2>Is this point on the line?</h2>
	<p>Given the line <strong>y = 2x + 1</strong>, is the point <strong>(3, 7)</strong> on the line?</p>
	<button class="expander" onclick="showSolution()">Show Solution</button>
	<div id="solution">
		<canvas id="graph"></canvas>
		<div id="answerText" style="margin-top:10px;"></div>
	</div>
	<script>
		function showSolution() {
			document.getElementById('solution').style.display = 'block';
			drawGraph();
			// Check if point (3,7) is on y = 2x + 1
			const x = 3, y = 7;
			const yOnLine = 2 * x + 1;
			const correct = y === yOnLine;
			document.getElementById('solution').style.background = correct ? '#c8f7c5' : '#f7c5c5';
			document.getElementById('answerText').innerHTML =
				correct
					? "<strong>Yes, the point (3, 7) is on the line y = 2x + 1.</strong><br>Because 2×3+1 = 7."
					: "<strong>No, the point (3, 7) is not on the line y = 2x + 1.</strong><br>Because 2×3+1 ≠ 7.";
		}

		function drawGraph() {
			const canvas = document.getElementById('graph');
			const ctx = canvas.getContext('2d');
			ctx.clearRect(0, 0, canvas.width, canvas.height);

			// Draw axes
			ctx.strokeStyle = '#000';
			ctx.beginPath();
			ctx.moveTo(30, 170); ctx.lineTo(270, 170); // x-axis
			ctx.moveTo(30, 170); ctx.lineTo(30, 30);   // y-axis
			ctx.stroke();

			// Draw line y = 2x + 1
			ctx.strokeStyle = '#0077cc';
			ctx.beginPath();
			for (let px = 30; px <= 270; px++) {
				let x = (px - 30) / 30; // scale: 1 unit = 30px
				let y = 2 * x + 1;
				let py = 170 - y * 20; // scale: 1 unit = 20px, invert y
				if (px === 30) ctx.moveTo(px, py);
				else ctx.lineTo(px, py);
			}
			ctx.stroke();

			// Draw point (3,7)
			let px = 30 + 3 * 30;
			let py = 170 - 7 * 20;
			ctx.beginPath();
			ctx.arc(px, py, 6, 0, 2 * Math.PI);
			ctx.fillStyle = '#e74c3c';
			ctx.fill();

			// Label point
			ctx.fillStyle = '#000';
			ctx.font = '14px Arial';
			ctx.fillText('(3,7)', px + 8, py - 8);
		}
	</script>
</body>
</html>
```
# first_slope