# M2 GDV les 2.2 (CODE) Peggle Game, Mikken en Line Rendering

![result](../src/2_2_Aim_Line_result.gif)

![import sprite](../src/2_2_import_sprite.png)

![apply](../src/2_1_import_sprite.png)

![create cannon](../src/2_2_create_cannon.gif)

Maak een script met de naam `Aim.cs` en hang die aan je `cannon holder`

```Csharp
using UnityEngine;

public class Aim : MonoBehaviour
{
    void Update()
    {
        Vector3 pos = Camera.main.WorldToScreenPoint(transform.position); //position of arrow on the screen
        Vector3 dir = Input.mousePosition - pos; //direction from arrow to cursor
        float angle = Mathf.Atan2(dir.y, dir.x) * Mathf.Rad2Deg;//calculate angle (radians naar degrees)
        transform.rotation = Quaternion.AngleAxis(angle, Vector3.forward);//rotate around one axis

    }
}
```
