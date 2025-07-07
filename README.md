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
![image of the player icon](https://www.google.com/url?sa=i&url=https%3A%2F%2Fes.pinterest.com%2Fpin%2F913878949359893335%2F&psig=AOvVaw1zLBw1oGLoSM-DnFJsrUx8&ust=1751940822134000&source=images&cd=vfe&opi=89978449&ved=0CBUQjRxqFwoTCNjHvqPWqY4DFQAAAAAdAAAAABAE)

![image of the platform or block](https://www.google.com/url?sa=i&url=https%3A%2F%2Fgeometry-dash.fandom.com%2Fwiki%2FObjects&psig=AOvVaw0UiRLPNupouO9kFfAVCPgt&ust=1751940922138000&source=images&cd=vfe&opi=89978449&ved=0CBUQjRxqFwoTCKD1kdTWqY4DFQAAAAAdAAAAABAE)

![image of the spike](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.deviantart.com%2Fgreaterhtrae%2Fart%2FSpike-1011766972&psig=AOvVaw1-YOKju8k2E_gHfQ9wA2xc&ust=1751940963057000&source=images&cd=vfe&opi=89978449&ved=0CBUQjRxqFwoTCOjNh-fWqY4DFQAAAAAdAAAAABAE)

![image of the coin](https://i.redd.it/whats-the-worst-coin-in-gd-including-subzero-meltdown-and-v0-uz6s5vwxanxc1.jpg?width=750&format=pjpg&auto=webp&s=f976f0eb80a08c42ddc9dbf61bd76e6c91002e57)
 


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
