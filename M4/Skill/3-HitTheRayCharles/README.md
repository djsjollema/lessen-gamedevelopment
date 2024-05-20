# M4.2 Hit the ray Charles


## Doelstelling
Leren werken met de raycast2D

## Context
Op een 2d-scherm rijdt een animatie van een enemy-tank naar een willekeurige plek op het scherm en schiet een projectiel af
 
## De opdracht

## Aangeboden Assets
Opdrachten tot zover (Tank en EnemyTank)
[zip bestand](Assets/TankGame.zip)



# het aanbieden van een Raycast2D 

In Unity kan je een Physics2D.raycast-object aanbieden:

````csharp
     RaycastHit2D hit = Physics2D.Raycast(position, direction, length);
````
deze object retourneert een RaycastHit2D-object 


````csharp
        if (hit.collider != null)
        {
            //
        }
````

Het RaycastHit2D-object heeft de volgende eigenschappen


| property	| description           |
| --------- | ------------------------------------------------------------------|
| centroid	| The centroid of the primitive used to perform the cast.           |
| collider	| The collider hit by the ray.                                      |
| distance	| The distance from the ray origin to the impact point.             |
| fraction	| Fraction of the distance along the ray that the hit occurred.     |
| normal	| The normal vector of the surface hit by the ray.                  |
| point	    | The point in world space where the ray hit the collider's surface.|
| rigidbody	| The Rigidbody2D attached to the object that was hit.              |
| transform	| The Transform of the object that was hit.                         |