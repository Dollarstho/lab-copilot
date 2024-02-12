## Input
crie uma algoritmo de geração de mapa procedural em C# para Unity.

## Output

Claro! Vou criar um algoritmo simples de geração de mapa procedural em C# para Unity. Neste exemplo, usaremos o Perlin Noise para criar um terreno montanhoso. Vamos lá:

```csharp
using UnityEngine;

public class MapGenerator : MonoBehaviour
{
    public int width = 256;
    public int height = 256;
    public float scale = 20f;

    private void Start()
    {
        GenerateMap();
    }

    private void GenerateMap()
    {
        Terrain terrain = GetComponent<Terrain>();
        terrain.terrainData = GenerateTerrain(terrain.terrainData);
    }

    private TerrainData GenerateTerrain(TerrainData terrainData)
    {
        terrainData.heightmapResolution = width + 1;
        terrainData.size = new Vector3(width, 10, height);
        terrainData.SetHeights(0, 0, GenerateHeights());
        return terrainData;
    }

    private float[,] GenerateHeights()
    {
        float[,] heights = new float[width, height];
        Vector2 offset = new Vector2(Random.Range(0f, 9999f), Random.Range(0f, 9999f));

        for (int x = 0; x < width; x++)
        {
            for (int y = 0; y < height; y++)
            {
                float xCoord = (float)x / width * scale + offset.x;
                float yCoord = (float)y / height * scale + offset.y;
                heights[x, y] = Mathf.PerlinNoise(xCoord, yCoord);
            }
        }

        return heights;
    }
}
```

Neste script:
- `width` e `height` definem o tamanho do terreno.
- `scale` controla a rugosidade do terreno.
- Usamos o Perlin Noise para gerar alturas aleatórias.

Lembre-se de anexar este script a um objeto com um componente `Terrain` no Unity. Você pode ajustar os parâmetros conforme necessário para obter diferentes resultados. Divirta-se criando seus próprios mapas! 🗺️🌄