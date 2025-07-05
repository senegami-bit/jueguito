🟦 Game Title: Spike Sprint
👥 Team: George Mena, Uriel Aguilar

🎮 Game Description:
Spike Sprint is a fast-paced obstacle game inspired by Geometry Dash and The Impossible Game. The player controls the cube to jump over obstucles and dangerous spikes. The goal is to try to complete the levels without dying and collecting 3 coins on levels.

Mechanics used:
Automatic foward movement
Up-Arrow, Space Bar or Mouse click
Collision detection on obstucles
Restarting on player's death
Level Progression
Coin collecting

📦 Resources Used
Assets:
Sprites: Player Icon Cube, spikes, blocks, and coins

🗺️ Scene Descriptions
Tutorial/Level 1:
Basic Movement and jumping over blocks, introducing the game mechanic for jumping.

Level 2:
Spikes are introduced and makes the level harder to pass, jumping over obstucles and collecting 3 coins on hard areas.
Death: Player dies, shows the area where they died and restarts the level to the beginning.
Player: Icon rotates on jumping or falling


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

 transition

func _on_timer_timeout() -> void:
	get_tree().reload_current_scene()

 func _on_puerta_body_entered(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://escenario/NIVEL2.tscn")
	pass # Replace with function body. 
