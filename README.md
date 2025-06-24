extends CharacterBody2D


const SPEED = 35500
const JUMP_VELOCITY = -1000

var gravedad = 4100


func _physics_process(delta: float) -> void:
	#gravedad
	if not is_on_floor():
		velocity += get_gravity() * delta

	#salto
	if Input.is_action_pressed("salto") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	velocity.x = SPEED * delta

	move_and_slide()
George

el codigo para rotation del jugador
$Sprite2D.rotation_degrees += 380 * delta
	else :
		var modulo = int($Sprite2D.rotation_degrees) % 90;
	
		if modulo > 45 :
			$Sprite2D.rotation_degrees += (90 - modulo)
		else :
			$Sprite2D.rotation_degrees -= modulo
