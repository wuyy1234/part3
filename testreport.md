# test report

``` 
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;

import info.gridworld.actor.Actor;
import info.gridworld.actor.ActorWorld;
import info.gridworld.actor.Bug;
import info.gridworld.actor.Flower;
import info.gridworld.actor.Rock;
import info.gridworld.grid.Grid;
import info.gridworld.grid.Location;

public class JumperTest {
	Jumper jumperTest=new Jumper();
	Rock rock=new Rock();
	Bug bug=new Bug();
	ActorWorld world = new ActorWorld();
	Flower flower=new Flower();
	Location loc1=new Location( 6,8 );
	@Test
	void test() {
		//先设置其在(8, 8)
		world.add(new Location(8, 8),jumperTest );
		assertEquals( 8 , jumperTest.getLocation().getRow() );
		
		world.add(new Location(6, 8),flower );
		world.add(new Location(4, 8),bug );
    //put a bug at (4,8)
		
		Grid<Actor> grid=jumperTest.getGrid();
		assert(grid.get(loc1) instanceof Flower  );
		//test the location contain a flower.
			
		world.add(new Location(7, 8),rock );
		//put a rock in front of him to block its way
		
		jumperTest.act();//jump to (6,8);
		
		assertEquals(6,jumperTest.getLocation().getRow());
    //test result shows that it jump the rock in front of it
		
		jumperTest.act();//intend to jump to (4,8),but a bug stop it
		jumperTest.act();
		jumperTest.act();
		jumperTest.act();
		assertEquals(180,jumperTest.getDirection());
		assertEquals(6,jumperTest.getLocation().getRow());
		//jumper turns 180 degrees to avoid the edge of the grid
		
		jumperTest.act();
		assertEquals(8,jumperTest.getLocation().getRow());
		
		
		assert(grid.get(loc1) ==null  );
		//the flower is removed 
		
		
	}

}

```
