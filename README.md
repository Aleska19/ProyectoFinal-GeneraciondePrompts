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
      "cell_type": "markdown",
      "source": [
        "# ProyectoFinal-GeneraciondePrompts\n",
        "# *SIMULADOR DE GASTOS PERSONALES*\n",
        "\n",
        "###### *RESUMEN*\n",
        "\n",
        "El proyecto “Simulador de Gastos” busca ayudar a los usuarios a gestionar sus finanzas personales mediante un análisis detallado de ingresos y gastos. Utilizando OpenAI GPT-4 API y DALL-E API, el simulador genera recomendaciones personalizadas y representaciones gráficas visuales para que los usuarios comprendan mejor su situación económica. Está desarrollado en Python y ejecutado en el entorno Google Colab, aprovechando su capacidad colaborativa y facilidad de uso.\n",
        "\n",
        "###### *INTRODUCCIÓN*\n",
        "\n",
        "La administración financiera personal es clave para alcanzar objetivos y mantener estabilidad económica. Sin embargo, muchas personas carecen de herramientas adecuadas para analizar sus gastos e ingresos. Este proyecto aborda esa necesidad, proporcionando un simulador que combina inteligencia artificial con visualizaciones gráficas, ayudando a los usuarios a tomar decisiones financieras más informadas.\n",
        "\n",
        "El usuario puede ingresar información sobre ingresos y gastos en diferentes categorías, y el sistema analizará estos datos para generar un resumen financiero, recomendaciones específicas y gráficos visuales.\n",
        "\n",
        "###### *OBJETIVO*\n",
        "\n",
        "El objetivo del “Simulador de Gastos” es:\n",
        "-  Ayudar a los usuarios a gestionar eficientemente sus finanzas personales.\n",
        "-  Generar recomendaciones personalizadas basadas en el análisis de sus ingresos y gastos.\n",
        "- Crear representaciones visuales que faciliten la comprensión de los datos financieros del usuario.\n",
        "\n",
        "###### *METODOLOGÍA*\n",
        "1. Ingreso de datos: El usuario introduce ingresos y clasifica sus gastos en categorías como vivienda, alimentación, transporte, etc.\n",
        "2.  Análisis de datos:\n",
        "- Los datos ingresados son procesados con Python.\n",
        "- OpenAI GPT-4 API genera recomendaciones personalizadas basadas en el análisis de los datos.\n",
        "3. Visualización gráfica:\n",
        "- Se generan gráficos utilizando bibliotecas como matplotlib o seaborn para mostrar la distribución de gastos.\n",
        "- DALL-E API crea imágenes relacionadas con los hábitos financieros del usuario.\n",
        "4. Presentación de resultados: El usuario visualiza un resumen financiero, recomendaciones y gráficos directamente en el entorno interactivo de Google Colab.\n",
        "\n",
        "###### *HERRAMIENTAS*\n",
        "- Python: Lenguaje principal para desarrollar el proyecto.\n",
        "- Google Colab: Entorno colaborativo para ejecutar y compartir el simulador.\n",
        "- OpenAI GPT-4 API: Para generar recomendaciones financieras personalizadas.\n",
        "- OpenAI DALL-E API: Para crear imágenes artísticas relacionadas con la gestión financiera.\n",
        "- Matplotlib/Seaborn: Para generar gráficos representativos de los datos."
      ],
      "metadata": {
        "id": "ZjFeSYy69F1V"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "pip install --upgrade openai"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "6PSh0N401JqG",
        "outputId": "0d132c4d-0eeb-43bc-e5d3-cb29e5275f3d"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Requirement already satisfied: openai in /usr/local/lib/python3.10/dist-packages (1.54.5)\n",
            "Collecting openai\n",
            "  Downloading openai-1.57.0-py3-none-any.whl.metadata (24 kB)\n",
            "Requirement already satisfied: anyio<5,>=3.5.0 in /usr/local/lib/python3.10/dist-packages (from openai) (3.7.1)\n",
            "Requirement already satisfied: distro<2,>=1.7.0 in /usr/local/lib/python3.10/dist-packages (from openai) (1.9.0)\n",
            "Requirement already satisfied: httpx<1,>=0.23.0 in /usr/local/lib/python3.10/dist-packages (from openai) (0.28.0)\n",
            "Requirement already satisfied: jiter<1,>=0.4.0 in /usr/local/lib/python3.10/dist-packages (from openai) (0.8.0)\n",
            "Requirement already satisfied: pydantic<3,>=1.9.0 in /usr/local/lib/python3.10/dist-packages (from openai) (2.10.3)\n",
            "Requirement already satisfied: sniffio in /usr/local/lib/python3.10/dist-packages (from openai) (1.3.1)\n",
            "Requirement already satisfied: tqdm>4 in /usr/local/lib/python3.10/dist-packages (from openai) (4.66.6)\n",
            "Requirement already satisfied: typing-extensions<5,>=4.11 in /usr/local/lib/python3.10/dist-packages (from openai) (4.12.2)\n",
            "Requirement already satisfied: idna>=2.8 in /usr/local/lib/python3.10/dist-packages (from anyio<5,>=3.5.0->openai) (3.10)\n",
            "Requirement already satisfied: exceptiongroup in /usr/local/lib/python3.10/dist-packages (from anyio<5,>=3.5.0->openai) (1.2.2)\n",
            "Requirement already satisfied: certifi in /usr/local/lib/python3.10/dist-packages (from httpx<1,>=0.23.0->openai) (2024.8.30)\n",
            "Requirement already satisfied: httpcore==1.* in /usr/local/lib/python3.10/dist-packages (from httpx<1,>=0.23.0->openai) (1.0.7)\n",
            "Requirement already satisfied: h11<0.15,>=0.13 in /usr/local/lib/python3.10/dist-packages (from httpcore==1.*->httpx<1,>=0.23.0->openai) (0.14.0)\n",
            "Requirement already satisfied: annotated-types>=0.6.0 in /usr/local/lib/python3.10/dist-packages (from pydantic<3,>=1.9.0->openai) (0.7.0)\n",
            "Requirement already satisfied: pydantic-core==2.27.1 in /usr/local/lib/python3.10/dist-packages (from pydantic<3,>=1.9.0->openai) (2.27.1)\n",
            "Downloading openai-1.57.0-py3-none-any.whl (389 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m389.9/389.9 kB\u001b[0m \u001b[31m7.6 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hInstalling collected packages: openai\n",
            "  Attempting uninstall: openai\n",
            "    Found existing installation: openai 1.54.5\n",
            "    Uninstalling openai-1.54.5:\n",
            "      Successfully uninstalled openai-1.54.5\n",
            "Successfully installed openai-1.57.0\n"
          ]
        }
      ]
    },
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
        "    display(Image(url=url_imagen))\n",
        "else:\n",
        "    print(\"\\nError al generar imagen:\", url_imagen)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "KdiTT2P6_umv",
        "outputId": "636260d1-9248-4666-bae1-d90f13108f85"
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
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "n96oKm0l3PNT"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
