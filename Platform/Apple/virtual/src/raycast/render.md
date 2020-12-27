



umul_bb_b
; Multiply two bytes, quickly but somewhat inaccurately, using logarithms fixed precision base 2 logarithms.
; Utilizes tbl_log2_b_b and tbl_pow2_b_b, which translate to and from 3+5 bit
; Input : unsigned bytes in X and Y
; Output: unsigned byte in A of the *high* byte of the result only


log2_w_w
; Calculate log2 of a 16-bit number.
; Input: 16-bit unsigned int in A(lo)/X(hi)
; Output: fixed point 8+8 bit log2 in A(lo)/X(hi)


log2_b_w
; Calculate log2 of a 8-bit number.
; Input: 8-bit unsigned byte in A
; Output: fixed point 8+8 bit log2 in A(lo)/X(hi)


pow2_w_w
; Calculate 2^n for a fixed-point n
; Input:  8.8 fixed precision number in Y(lo)/X(hi)
; Output: 16 bit unsigned int in A(lo)/X(hi)


sinTbl=[
	  0x0000, 0x8699, 0x877F, 0x87E1, 0x8800, 0x87E1, 0x877F, 0x8699
	, 0x8195, 0x0699, 0x077F, 0x07E1, 0x0800, 0x07E1, 0x077F, 0x0699
]


https://lodev.org/cgtutor/raycasting.html


player = {
  x : 4.2421875,      // current x, y position
  y : 6.4765625,
  dir : 0,    // the direction that the player is turning, either -1 for left or 1 for right.
  angleNum : 0xA, // the current angle of rotation
  speed : 0,    // is the playing moving forward (speed = 1) or backwards (speed = -1).
  // how far (in map units) does the player move each step/update
  moveSpeed : 0.25,  
  // how much does the player rotate each step/update (in radians)
  rotSpeed : 22.5 * Math.PI / 180, // 22.5 = 360 deg / 16 angles
  strafe: false
}

angleNum [0..15]
x [0..62]

precastData[angleNum][x] = {
    rayDirX: [], 
    rayDirY: [],
    deltaDistX: [],
    deltaDistY: [] }

prepCast(angleNum, x)
renvoie

angle               = angleNum * player.rotSpeed;
dirX, dirY          = cos(angle), sin(angle)
planeX, planeY      = -sin(angle) * 0.5, cos (angle)*0.5
// x-coordinate in camera space
cameraX             = 2 * x / 63 - 1;
rayDirX, rayDirY    = dirX + planeX * cameraX, dirY + planeY * cameraX

deltaDistX          = Math.sqrt(1 + (rayDirY * rayDirY) / (rayDirX * rayDirX))
deltaDistY          = Math.sqrt(1 + (rayDirX * rayDirX) / (rayDirY * rayDirY))

angle (radians)