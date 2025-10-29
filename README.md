# UnityEmissionFormula

Эта формула была выведена пользователем **W8WHILE** для корректного расчёта **HDR Emission Intensity** в Unity.  

---

## Формула

**Y ≈ 3.32 · log10(X) + 0.93**

- **X** — значение красного канала (`_EmissionColor.r`) материала в HDR (можно использовать любую компоненту RGB или их сумму).  
- **Y** — Intensity, как отображается в инспекторе Unity.  

Эта формула помогает преобразовать цвет HDR в визуальную интенсивность свечения, учитывая, как Unity Standard Shader отображает Emission.

---
Применение

Реалтайм изменение Emission для светящихся объектов.

Точная настройка яркости в HDR сценах.

Совместимо со стандартным шейдером Unity и URP Lit Shader.

## Пример использования на C#

```csharp
using UnityEngine;

public class EmissionExample : MonoBehaviour
{
    [SerializeField] private Material material;
    [SerializeField] private Color baseColor = Color.white;
    [SerializeField] private float intensity = 10f;

    void UpdateEmission()
    {
        // Вычисляем HDR цвет с учётом формулы W8WHILE
        float factor = Mathf.Pow(10f, (intensity - 0.93f) / 3.32f);
        Color hdrColor = baseColor.linear * factor;
        hdrColor.a = 1f;

        material.SetColor("_EmissionColor", hdrColor);
    }
}
