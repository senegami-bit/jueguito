# 🟦 Game Title: Spike Sprint

# 👥 Team: George Mena, Uriel Aguilar

# 🎮 Game Description:
Spike Sprint is a fast-paced obstacle game inspired by Geometry Dash and The Impossible Game. 
The player controls the cube to jump over obstucles and dangerous spikes. 
The goal is to try to complete the levels without dying and collecting 3 coins on levels.

# Mechanics used:
Automatic foward movement
Up-Arrow, Space Bar or Mouse click
Collision detection on obstucles
Restarting on player's death
Level Progression
Coin collecting

# 📦 Resources Used
Assets:

 # Images
![image of the player icon](https://i.pinimg.com/474x/dd/b4/b2/ddb4b288d3eb1b7b669e77e3d21f9566.jpg)

![image of the platform or block](https://static.wikia.nocookie.net/geometry-dash/images/0/01/RegularBlock01.png/revision/latest?cb=20160604070948)

![image of the spike](https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/2f961ba4-4243-4889-928c-e7f4c2d38614/dgqdoe4-e953f151-5935-4e8c-a24c-7b29b8a09b8a.png/v1/fill/w_285,h_284/spike_by_greaterhtrae_dgqdoe4-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7ImhlaWdodCI6Ijw9Mjg0IiwicGF0aCI6IlwvZlwvMmY5NjFiYTQtNDI0My00ODg5LTkyOGMtZTdmNGMyZDM4NjE0XC9kZ3Fkb2U0LWU5NTNmMTUxLTU5M)

![image of the coin](https://image.pngaaa.com/688/3664688-middle.png)
 


# 🗺️ Scene Descriptions
Tutorial/Level 1:
Basic Movement and jumping over blocks, introducing the game mechanic for jumping.

# Level 2:
Spikes are introduced and makes the level harder to pass, jumping over obstucles and collecting 3 coins on hard areas.
Death: Player dies, shows the area where they died and restarts the level to the beginning.
Player: Icon rotates on jumping or falling


# 🧑‍💻 Code Descriptions

player.gd


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

    $Sprite2D.rotation_degrees += 380 * delta
	else :
		var modulo = int($Sprite2D.rotation_degrees) % 90;
	
		if modulo > 45 :
			$Sprite2D.rotation_degrees += (90 - modulo)
		else :
			$Sprite2D.rotation_degrees -= modulo

  
  # Spike.gd
   
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
 
transition.gd

    func _on_timer_timeout() -> void:
	get_tree().reload_current_scene()

    func _on_puerta_body_entered(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://escenario/NIVEL2.tscn")
	pass # Replace with function body. 

# 🛠️ Difficulties Encountered Using Collaborative Tools

 George: I had difficulty running the game and had issues with assets not working. It took me 30 mins to figure out how to collect coins and make the player speed
 and gravity to be perfect. For the coin, I couldn't figure how to collect coin to be labeled on the top left.


Collaborator 2: Uriel
