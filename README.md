George
codigo para el movimiento y el  brinco para el jugador:

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

el codigo para rotation del jugador:

$Sprite2D.rotation_degrees += 380 * delta
	else :
		var modulo = int($Sprite2D.rotation_degrees) % 90;
	
		if modulo > 45 :
			$Sprite2D.rotation_degrees += (90 - modulo)
		else :
			$Sprite2D.rotation_degrees -= modulo

   George
   el codigo para el muerto del jugador cuando se pega a un pincha (spike) o bloque:
   
   extends Area2D

func _on_body_entered(body):
	if body.is_in_group("kill") :
		$"..".death()
		self.queue_free()
  
y para externo muerte:
extends Area2D

func _on_area_entered(area: Area2D) -> void:
	if area.is_in_group("kill") :
		$"..".death()
		self.queue_free()
  
tambien hizo un cambio del jugador para un nuevo hitbox de muerte para los pinchas (spikes):
func death():
	SPEED = 0
	$Sprite2D.visible = false
	$Timer.start()
	

func _on_timer_timeout() -> void:
	get_tree().reload_current_scene()
