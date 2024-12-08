# ProyectoFinal-GeneraciondePrompts
# *SIMULADOR DE GASTOS PERSONALES*

###### *RESUMEN*

El proyecto “Simulador de Gastos” busca ayudar a los usuarios a gestionar sus finanzas personales mediante un análisis detallado de ingresos y gastos. Utilizando OpenAI GPT-4 API y DALL-E API, el simulador genera recomendaciones personalizadas y representaciones gráficas visuales para que los usuarios comprendan mejor su situación económica. Está desarrollado en Python y ejecutado en el entorno Google Colab, aprovechando su capacidad colaborativa y facilidad de uso.

###### *INTRODUCCIÓN*

La administración financiera personal es clave para alcanzar objetivos y mantener estabilidad económica. Sin embargo, muchas personas carecen de herramientas adecuadas para analizar sus gastos e ingresos. Este proyecto aborda esa necesidad, proporcionando un simulador que combina inteligencia artificial con visualizaciones gráficas, ayudando a los usuarios a tomar decisiones financieras más informadas.

El usuario puede ingresar información sobre ingresos y gastos en diferentes categorías, y el sistema analizará estos datos para generar un resumen financiero, recomendaciones específicas y gráficos visuales.

###### *OBJETIVO*

El objetivo del “Simulador de Gastos” es:
-  Ayudar a los usuarios a gestionar eficientemente sus finanzas personales.
-  Generar recomendaciones personalizadas basadas en el análisis de sus ingresos y gastos.
- Crear representaciones visuales que faciliten la comprensión de los datos financieros del usuario.

###### *METODOLOGÍA*
1. Ingreso de datos: El usuario introduce ingresos y clasifica sus gastos en categorías como vivienda, alimentación, transporte, etc.
2.  Análisis de datos:
- Los datos ingresados son procesados con Python.
- OpenAI GPT-4 API genera recomendaciones personalizadas basadas en el análisis de los datos.
3. Visualización gráfica:
- Se generan gráficos utilizando bibliotecas como matplotlib o seaborn para mostrar la distribución de gastos.
- DALL-E API crea imágenes relacionadas con los hábitos financieros del usuario.
4. Presentación de resultados: El usuario visualiza un resumen financiero, recomendaciones y gráficos directamente en el entorno interactivo de Google Colab.

###### *HERRAMIENTAS*
- Python: Lenguaje principal para desarrollar el proyecto.
- Google Colab: Entorno colaborativo para ejecutar y compartir el simulador.
- OpenAI GPT-4 API: Para generar recomendaciones financieras personalizadas.
- OpenAI DALL-E API: Para crear imágenes artísticas relacionadas con la gestión financiera.
- Matplotlib/Seaborn: Para generar gráficos representativos de los datos.



{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "ckOailXGrgjl"
      },
      "outputs": [],
      "source": [
        "pip install openai matplotlib pandas\n"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "import openai\n",
        "import pandas as pd\n",
        "import matplotlib.pyplot as plt\n"
      ],
      "metadata": {
        "id": "2DzO3NT8rn9M"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "openai.api_key = \"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\""
      ],
      "metadata": {
        "id": "g2S8p9sD9LQu"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "def obtener_recomendaciones(mensaje):\n",
        "    try:\n",
        "        respuesta = openai.ChatCompletion.create(\n",
        "            model=\"gpt-4\",\n",
        "            messages=[\n",
        "                {\"role\": \"system\", \"content\": \"Eres un asesor financiero experto.\"},\n",
        "                {\"role\": \"user\", \"content\": mensaje},\n",
        "            ],\n",
        "            max_tokens=200,\n",
        "        )\n",
        "        return respuesta[\"choices\"][0][\"message\"][\"content\"]\n",
        "    except Exception as e:\n",
        "        return f\"Error al conectar con GPT-4: {e}\"\n",
        "\n",
        "def generar_imagen(prompt):\n",
        "    try:\n",
        "        respuesta = openai.Image.create(\n",
        "            prompt=prompt,\n",
        "            n=1,\n",
        "            size=\"1024x1024\"\n",
        "        )\n",
        "        return respuesta[\"data\"][0][\"url\"]\n",
        "    except Exception as e:\n",
        "        return f\"Error al generar imagen: {e}\"\n"
      ],
      "metadata": {
        "id": "JmIEz4zm_oOZ"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "print(\"Bienvenido al simulador de gastos.\")\n",
        "ingresos = float(input(\"Ingresa tus ingresos mensuales: \"))\n",
        "categorias = [\"Alquiler\", \"Comida\", \"Transporte\", \"Entretenimiento\", \"Otros\"]\n",
        "gastos = {}\n",
        "\n",
        "for categoria in categorias:\n",
        "    gastos[categoria] = float(input(f\"Ingresa tus gastos en {categoria}: \"))\n",
        "\n",
        "# Paso 5: Análisis de datos\n",
        "total_gastos = sum(gastos.values())\n",
        "saldo = ingresos - total_gastos\n",
        "\n",
        "# Mostrar resultados\n",
        "print(\"\\nResumen Financiero:\")\n",
        "print(f\"Ingresos: ${ingresos}\")\n",
        "print(f\"Gastos totales: ${total_gastos}\")\n",
        "print(f\"Saldo final: ${saldo}\")\n",
        "\n",
        "# Paso 6: Visualización gráfica\n",
        "df = pd.DataFrame(list(gastos.items()), columns=[\"Categoría\", \"Gasto\"])\n",
        "df.set_index(\"Categoría\", inplace=True)\n",
        "\n",
        "# Gráfico de barras\n",
        "df.plot(kind=\"bar\", legend=False, title=\"Distribución de Gastos\", color=\"skyblue\")\n",
        "plt.ylabel(\"Gasto ($)\")\n",
        "plt.show()\n",
        "\n",
        "# Gráfico de torta\n",
        "df.plot(kind=\"pie\", y=\"Gasto\", autopct=\"%1.1f%%\", legend=False, title=\"Gastos por Categoría\")\n",
        "plt.ylabel(\"\")\n",
        "plt.show()\n",
        "\n",
        "# Paso 7: Recomendaciones con GPT-4\n",
        "mensaje_usuario = f\"Tengo un saldo de ${saldo} después de gastos de ${total_gastos}. ¿Qué recomendaciones me das para mejorar mis finanzas?\"\n",
        "recomendaciones = obtener_recomendaciones(mensaje_usuario)\n",
        "print(\"\\nRecomendaciones de GPT-4:\")\n",
        "print(recomendaciones)\n",
        "\n",
        "# Paso 8: Generar imagen con DALL-E\n",
        "prompt_imagen = \"Una representación artística de la gestión de finanzas personales con categorías como ahorro, inversión y gastos diarios.\"\n",
        "url_imagen = generar_imagen(prompt_imagen)\n",
        "if \"http\" in url_imagen:\n",
        "    print(\"\\nImagen generada por DALL-E:\")\n",
        "    print(url_imagen)\n",
        "    display(Image(url_imagen))  # Muestra la imagen directamente en Google Colab\n",
        "else:\n",
        "    print(\"\\nError al generar imagen:\", url_imagen)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 0
        },
        "id": "KdiTT2P6_umv",
        "outputId": "76f66075-15b0-4987-b7dd-cae4af5a5aed"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Bienvenido al simulador de gastos.\n"
          ]
        }
      ]
    }
  ]
}


