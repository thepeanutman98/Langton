# Langton

var canvas = document.getElementById('canvas'); var ctx = canvas.getContext('2d'); var grid = {cells: {}, draw: function(){ctx.clearRect(0,0,canvas.width,canvas.width); for (var y = 0; y < canvas.height/10; y ++) {for (var x = 0; x < canvas.width/10; x ++) {
switch (grid.cells[x+','+y]) {
    case 1:
		ctx.beginPath();
		ctx.lineWidth="1";
		ctx.strokeStyle="grey";
		ctx.fillStyle='#FF9900';
		ctx.fillRect(x*10,y*10,10,10);
		ctx.stroke();
		break;
}
ctx.beginPath();
ctx.rect(x*10,y*10,10,10);
ctx.stroke();}}}, turtle: {tick: function() {this.x += this.dirX; this.y += this.dirY; this.dir += this.parent.cells[this.x + ',' + this.y] ? -1 : 1; this.dir %= 4; this.dir = this.dir == -1 ? 0 : this.dir; this.parent.cells[this.x + ',' + this.y] ^= 1}, x: 50, y: 50, dir: 1, get dirX() {return ((this.dir == 0 || this.dir == 2) ? 0 : (this.dir == 1 ? 1 : (this.dir == 3 ? -1 : null)))}, get dirY() {return (this.dir == 1 || this.dir == 3) ? 0 : (this.dir == 0 ? -1 : (this.dir == 2 ? 1 : null))}}, init : function() {
        this.turtle.parent = this;
        delete this.init;
        return this;
    }}.init()
grid.draw()
undefined
var tick = setInterval(function(){grid.turtle.tick(); grid.draw()},1)
undefined
clearInterval(tick)



var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
var grid = {
    cells: {},
	cellSize: 10,
	tickTime: 1,
	ticksPerDraw: 1,
    draw: function() {
        ctx.clearRect(0, 0, canvas.width, canvas.width);
        for (var y = 0; y < canvas.height / this.cellSize; y++) {
            for (var x = 0; x < canvas.width / this.cellSize; x++) {
                switch (grid.cells[x + ',' + y]) {
                case 1:
                    ctx.beginPath();
                    ctx.lineWidth = "1";
                    ctx.strokeStyle = "grey";
                    ctx.fillStyle = '#FF9900';
                    ctx.fillRect(x * this.cellSize, y * this.cellSize, this.cellSize, this.cellSize);
                    ctx.stroke();
                    break;
                }
        }
        }
		ctx.beginPath();
        ctx.lineWidth = "1";
        ctx.strokeStyle = "grey";
        ctx.fillStyle = '#0055FF';
        ctx.fillRect(this.turtle.x * this.cellSize, this.turtle.y * this.cellSize, this.cellSize, this.cellSize);
        ctx.stroke();
    },
    turtle: {
        tick: function() {
            this.x += this.dirX;
            this.y += this.dirY;
			if (this.x > canvas.width) {
				this.x = 0;
				this.y = canvas.height - this.y;
            } else if (this.x < 0) {
				this.x = canvas.width;
				this.y = canvas.height - this.y;
            } else if (this.y > canvas.height) {
				this.y = 0;
				this.x = canvas.width - this.x;
            } else if (this.y < 0) {
				this.y = canvas.height;
				this.x = canvas.width - this.x;
            }
            this.dir += this.parent.cells[this.x + ',' + this.y] ? -1 : 1;
            this.dir %= 4;
            this.dir = this.dir == -1 ? 3 : this.dir;
            this.parent.cells[this.x + ',' + this.y] ^= 1
        },
        x: 50,
        y: 50,
        dir: 1,
        get dirX() {
            return ( (this.dir == 0 || this.dir == 2) ? 0 : (this.dir == 1 ? 1 : (this.dir == 3 ? -1 : null)))
        },
        get dirY() {
            return (this.dir == 1 || this.dir == 3) ? 0 : (this.dir == 0 ? -1 : (this.dir == 2 ? 1 : null))
        }
    },
    init: function() {
        this.turtle.parent = this;
        delete this.init;
        return this;
    }
}.init();
grid.draw()
