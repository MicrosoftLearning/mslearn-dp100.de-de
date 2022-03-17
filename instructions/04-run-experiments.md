---
lab:
  title: Ausführen von Experimenten
ms.openlocfilehash: 62b6b79c99142d4311c2d9c0db4b02cfd710feb6
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2022
ms.locfileid: "138597273"
---
# <a name="run-experiments"></a>Ausführen von Experimenten

Experimente sind der Kern der Arbeit einer wissenschaftlichen Fachkraft für Daten. In Azure Machine Learning wird ein *Experiment* zum Ausführen eines Skripts oder einer Pipeline verwendet und generiert normalerweise Ausgaben und zeichnet Metriken auf. In dieser Übung verwenden Sie das Azure Machine Learning SDK, um Python-Code als Experimente durchzuführen.

## <a name="before-you-start"></a>Vorbereitung

Sofern nicht bereits geschehen, bearbeiten Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* , um einen Azure Machine Learning-Arbeitsbereich und eine Compute-Instanz zu erstellen und die für diese Übung benötigten Notebooks zu klonen.

## <a name="open-jupyter"></a>Öffnen von Jupyter

Sie können zwar die Seite **Notebooks** in Azure Machine Learning Studio zum Ausführen von Notebooks nutzen, doch erweist sich die Verwendung einer Notebookentwicklungsumgebung mit größerem Funktionsumfang wie *Jupyter* häufig als produktiver. Praktischerweise ist in Ihrer Azure Machine Learning-Compute-Instanz eine Installation von Jupyter enthalten.

> **Tipp**: Jupyter Notebook ist ein häufig verwendetes Open-Source-Tool für Data Science. Wenn Sie damit noch nicht vertraut sind, sehen Sie sich die [Dokumentation](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html) an.

1. Zeigen Sie in [Azure Machine Learning Studio](https://ml.azure.com) die Seite **Compute** für Ihren Arbeitsbereich an, und starten Sie auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz, falls diese noch nicht ausgeführt wird.
2. Wenn die Compute-Instanz ausgeführt wird, klicken Sie auf den Link **Jupyter**, um die Jupyter-Startseite auf einer neuen Browserregisterkarte zu öffnen. Achten Sie darauf, dass Sie *Jupyter* und nicht *JupyterLab* öffnen.

> **Tipp**: Haben Sie noch keine Erfahrung mit Python? Das [Cheat Sheet für Python](cheat-sheets/dp100-cheat-sheet-python.pdf) hilft Ihnen dabei, den Code zu verstehen.

## <a name="verify-the-azure-machine-learning-sdk-is-installed"></a>Überprüfen der Installation von Azure Machine Learning SDK

Das Azure Machine Learning SDK wird standardmäßig auf Ihrer Compute-Instanz installiert. Führen Sie die folgenden Schritte aus, um die Installation zu überprüfen.

1. Erstellen Sie in der Jupyter Notebook-Umgebung ein neues **Terminal**. Dadurch wird eine neue Registerkarte mit einer Befehlsshell geöffnet.
2. Geben Sie den folgenden Befehl ein, um sicherzustellen, dass das Azure ML SDK installiert ist:

    ```bash
    pip show azureml-sdk
    ```

    Beachten Sie die Version des installierten SDK-Pakets.

3. Das SDK-Paket **azureml-sdk** stellt die wichtigsten Bibliotheken bereit, die für die Arbeit mit Azure Machine Learning erforderlich sind. Es gibt jedoch einige zusätzliche Pakete mit anderen nützlichen Bibliotheken, die nicht im Haupt-SDK-Paket enthalten sind. Verwenden Sie den folgenden Befehl, um zu überprüfen, ob das Paket **azureml-widgets** mit Bibliotheken zum Anzeigen von Azure Machine Learning-Informationen in Notebooks ebenfalls installiert ist:

    ```bash
    pip show azureml-widgets
    ```

4. Schließen Sie die Registerkarte **Terminal**, und kehren Sie zu der Registerkarte mit der Jupyter-Startseite zurück.

> **Weitere Informationen**: Weitere Informationen zum Installieren des Azure ML SDK und seiner optionalen Komponenten finden Sie in der [Dokumentation zum Azure ML SDK](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py).

## <a name="run-experiments-in-a-notebook"></a>Ausführen von Experimenten in einem Notebook

Experimente in Azure Machine Learning müssen von einer Art *Steuerungsebene* initiiert werden, häufig von einem Skript oder Programm. In dieser Übung verwenden Sie ein Notebook zum Steuern von Experimenten.

1. Navigieren Sie auf der Jupyter-Startseite zum Ordner **/users/*Ihr-Benutzername*/mslearn-dp100**, in dem Sie das Notebook-Repository geklont haben, und öffnen Sie das Notebook **Run Experiments** (Experimente ausführen).
2. Lesen Sie dann die Hinweise im Notebook, und führen Sie die einzelnen Codezellen nacheinander aus.
3. Nachdem Sie den Code im Notebook ausgeführt haben, klicken Sie im Menü **Datei** auf **Schließen und anhalten**, um das Notebook zu schließen und den Python-Kernel herunterzufahren. Schließen Sie dann alle Jupyter-Browserregisterkarten.

## <a name="clean-up"></a>Bereinigung

Wenn Sie die Arbeit mit Azure Machine Learning vorerst beendet haben, wählen Sie in Azure Machine Learning Studio auf der Seite **Compute** auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz aus, und klicken Sie auf **Beenden**, um sie herunterzufahren. Andernfalls führen Sie die Instanz für das nächste Lab weiter aus.

> **Hinweis**: Durch das Beenden Ihrer Compute-Instanz wird sichergestellt, dass Ihrem Abonnement keine Computeressourcen in Rechnung gestellt werden. Ihnen wird jedoch eine geringe Datenspeichermenge in Rechnung gestellt, solange der Azure Machine Learning-Arbeitsbereich in Ihrem Abonnement enthalten ist. Wenn Sie mit dem Erkunden von Azure Machine Learning fertig sind, können Sie Ihren Azure Machine Learning-Arbeitsbereich und die zugehörigen Ressourcen löschen. Wenn Sie jedoch weitere Labs in dieser Reihe durchführen möchten, müssen Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* wiederholen, um zunächst den Arbeitsbereich zu erstellen und die Umgebung vorzubereiten.