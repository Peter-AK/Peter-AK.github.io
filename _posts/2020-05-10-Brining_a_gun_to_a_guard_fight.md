---
layout: post
title: Bringing a gun to a guard fight<br> [Foobar with Google]

---

<table>
  	<tr>
    	<th style="text-align: center; vertical-align: middle;">
    		<img src="{{ site.baseurl }}/assets/img/posts/post1/aline_gun.png" height="110" style="border:5px solid black" align="middle">
    	</th>
    	<th>
    		<a href="https://github.com/peter-ak/google_foobar"><img src="https://gh-card.dev/repos/peter-ak/google_foobar.svg"></a>
    	</th>
  	</tr>
  	<tr>
    	<td colspan="2">
    		Level 4 question from the Google foobar challenge. How many ways can you hit a guard with a laser without hitting your-self? {Python}
		</td>
  	</tr>
</table>

<table>
  	<tr>
    	<td colspan="2" style="background-color:#eaeaea">
			<b>===============================</b>
			<p>
			Uh-oh - you've been cornered by one of Commander Lambdas elite guards! Fortunately, you grabbed a beam weapon from an abandoned guard post while you were running through
			</p>
			the station, so you have a chance to fight your way out. But the beam weapon is potentially dangerous to you as well as to the elite guard: its beams reflect off walls,
			meaning you'll have to be very careful where you shoot to avoid bouncing a shot toward yourself!
			<p>
			Luckily, the beams can only travel a certain maximum distance before becoming too weak to cause damage. You also know that if a beam hits a corner, it will bounce back in exactly the same direction. And of course, if the beam hits either you or the guard, it will stop immediately (albeit painfully).
			</p>
			<p>
			Write a function solution(dimensions, your_position, guard_position, distance) that gives an array of 2 integers of the width and height of the room, an array of 2 integers of your x and y coordinates in the room, an array of 2 integers of the guard's x and y coordinates in the room, and returns an integer of the number of distinct directions that you can fire to hit the elite guard, given the maximum distance that the beam can travel.
			</p>
			<p>
			The room has integer dimensions [1 < x_dim <= 1250, 1 < y_dim <= 1250]. You and the elite guard are both positioned on the integer lattice at different distinct positions (x, y) inside the room such that [0 < x < x_dim, 0 < y < y_dim]. Finally, the maximum distance that the beam can travel before becoming harmless will be given as an integer 1 < distance <= 10000.
			</p>
			<p>
			For example, if you and the elite guard were positioned in a room with dimensions [3, 2], your_position [1, 1], guard_position [2, 1], and a maximum shot distance of 4, you could shoot in seven different directions to hit the elite guard (given as vector bearings from your location): [1, 0], [1, 2], [1, -2], [3, 2], [3, -2], [-3, 2], and [-3, -2]. As specific examples, the shot at bearing [1, 0] is the straight line horizontal shot of distance 1, the shot at bearing [-3, -2] bounces off the left wall and then the bottom wall before hitting the elite guard with a total shot distance of sqrt(13), and the shot at bearing [1, 2] bounces off just the top wall before hitting the elite guard with a total shot distance of sqrt(5).
			</p>
			<br>Test cases
			<br>==========
			<br>Your code should pass the following test cases.
			<br>Note that it may also be run against hidden test cases not shown here.
			<br>
			<br>-- Python cases --
			<br>Input:
			<br>solution.solution([3,2], [1,1], [2,1], 4)
			<br>Output:
			<br>&nbsp;    7
			<br>
			<br>Input:
			<br>solution.solution([300,275], [150,150], [185,100], 500)
			<br>Output:
			<br>&nbsp;    9
		</td>
  	</tr>
  	<tr>
  		<td style="background-color:#d0d0a5">
  			<p><b>Analysis:</b> 
  			<br>Let us work with the given example in this problem: 
  			<br>Room Size [3, 2]; Player Location [1, 1]; Guard Location [2, 1] and a distance 4 units.</p>
  			<p> My first idea was to set a fix general coordinate system where x = 0 degrees and calculate the new angle each time the laser bounced off the wall.
  			Unfortunately I ran into a few problems with this idea, mainly that there can be an infinite amount of angles that you can shoot in.</p>
  			<p>The other approach is to mirror the room in question, to determine the possible locations of each guard and whether we can shoot him. This is the method that we will use. </p>
  		</td>
  		<td style="background-color:#d0d0a5">
  			<img src="{{ site.baseurl }}/assets/img/posts/post1/inital_example.png" height="320" width="500" style="border:2px solid black ; margin:0px 20px">
  			O = Player Position; X = Guard position <div align="right"> Figure 1.</div>
  		</td>
  	</tr>
  	<tr>
  		<td style="background-color:#d0d0a5">
  			<p>Figure 2. shows us that we have mirrored the room along the North wall. 
  				<br>Shooting the guard in the mirrored room is the equivalent of shooting the guard at 63 deg angle and have it bounce off the wall in the same room. [After the first bounce, the laser in the red has the same distance and angle as the laser in the white]</p>
  				<p><b>1) Get all the 1st quadrant's Guard + Player positions. (positive x; positive y)</b>
  				{% highlight js %}max_x = player_x_position + laser_distance{% endhighlight %}
  				5 = 1 + 4, the same goes for the y position.
  				{% highlight js %}ceil(max_x / room_x)  --> celing(5/3) = 2 {% endhighlight %}
  				{% highlight js %}ceil(max_y / room_y)  --> celing(5/2) = 3 {% endhighlight %}
  				As you can see, we need to perform mirror 3x along the y axis of the room, but only 2x along the x axis. (see Figure 3.)</p> 
  		</td>
  		<td style="background-color:#d0d0a5">
  			<img src="{{ site.baseurl }}/assets/img/posts/post1/mirror_ex.png" height="600" width="500" style="border:2px solid black ; margin:0px 20px">
  			<div align="right"> Figure 2.</div>
  		</td>
  	</tr>
    <tr>
      <td style="background-color:#d0d0a5">
        <p><b>2) Reflect the position of all the 1st quadrant to the other 3 quadrants.</b>
          <br>A list for each position was generated in the first step : <br> [x_coords, y_coords, Player = 1 or Guard = 7]
          {% highlight js %} position_list_first_quadrant = 
          [[1, 1, 1], [2, 1, 7], [2, 3, 7] ..] {% endhighlight %}</p>
          <p>
            We can simply multiply the x and y by the appropriate sign to get back all the other quadrants
            <br> 2nd Quadrant : [-1 * x, y]
            <br> 3nd Quadrant : [-1 * x, -1 * y]
            <br> 4nd Quadrant : [x, -1 * y]
          </p>
      </td>
      <td style="background-color:#d0d0a5">
        <div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post1/mirror_ex_fq.png" height="600" width="500" style="border:2px solid black"></div>
        <div align="right"> Figure 3.</div>
      </td>
    </tr>
    <tr>
      <td style="background-color:#d0d0a5">
        <p><b>3) Filter all the Player + Guard positions by distance.</b>
          </p>
      </td>
      <td style="background-color:#d0d0a5">
        <p><b>3) Filter all the Player + Guard positions by distance.</b>
          </p>
      </td>
    </tr>
    <tr>
      <td colspan="2" style="background-color:#d0d0a5">
        <div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post1/full_grid.png" height="750" width="750" style="border:2px solid black"></div>
        <div align="right"> Figure 3.</div>
      </td>
    </tr>
</table>

<!--   			<p>$$\sqrt {(x_2-x_1)^2 +(y_2-y_1)^2}$$</p> -->