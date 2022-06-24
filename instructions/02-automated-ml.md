---
lab:
  title: Verwenden von automatisiertem maschinellen Lernen
ms.openlocfilehash: 70580a25d4bcd3929697874650ea6865262871f4
ms.sourcegitcommit: d2354e40eec31c22eb09381c6a890311cccc30c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2022
ms.locfileid: "146266838"
---
# <a name="use-automated-machine-learning"></a>Verwenden von automatisiertem maschinellen Lernen

Azure Machine Learning umfasst eine Funktionalität für das *automatisierte maschinelle Lernen*, die die Skalierbarkeit des Cloudcomputing nutzt, um automatisch mehrere Vorverarbeitungstechniken und Modelltrainingsalgorithmen gleichzeitig auszuprobieren, um das beste überwachte Machine Learning-Modell für Ihre Daten zu ermitteln.

In dieser Übung verwenden Sie die grafische Benutzeroberfläche für automatisiertes maschinelles Lernen in Azure Machine Learning Studio.

> **Hinweis**: Sie können automatisiertes maschinelles Lernen auch über das Azure Machine Learning SDK verwenden.

## <a name="before-you-start"></a>Vorbereitung

Sofern nicht bereits geschehen, bearbeiten Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* , um einen Azure Machine Learning-Arbeitsbereich und eine Compute-Instanz zu erstellen und die für diese Übung benötigten Notebooks zu klonen.

## <a name="configure-compute-resources"></a>Konfigurieren von Computeressourcen

Um automatisiertes maschinelles Lernen verwenden zu können, benötigen Sie eine Computeressource, auf der Sie das Experiment zum Modelltraining durchführen.

1. Melden Sie sich mit den Ihrem Azure-Abonnement zugeordneten Microsoft-Anmeldedaten bei [Azure Machine Learning Studio](https://ml.azure.com?azure-portal=true) an, und wählen Sie Ihren Azure Machine Learning-Arbeitsbereich aus.
2. Zeigen Sie in Azure Machine Learning Studio die Seite **Compute** an, und starten Sie auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz, falls diese noch nicht ausgeführt wird. Sie verwenden diese Compute-Instanz, um Ihr trainiertes Modell zu testen.
3. Während die Compute-Instanz gestartet wird, wechseln Sie zur Registerkarte **Computecluster**, und fügen Sie einen neuen Computecluster mit den folgenden Einstellungen hinzu. Sie führen das Experiment für automatisiertes maschinelles Lernen in diesem Cluster aus, um die Möglichkeit zu nutzen, die Trainingsläufe auf mehrere Computeknoten zu verteilen:
    - **Standort**: *Derselbe Standort wie Ihr Arbeitsbereich*
    - **VM-Dienstebene:** Dedicated
    - **VM-Typ:** CPU
    - **VM-Größe:** Standard_DS11_v2
    - **Computename:** *Geben Sie einen eindeutigen Namen ein.*
    - **Mindestanzahl von Knoten:** 0
    - **Maximale Knotenanzahl:** 2
    - **Leerlauf in Sekunden vor dem Herunterskalieren:** 120
    - **Enable SSH access** (SSH-Zugriff aktivieren): Nicht ausgewählt

## <a name="create-a-dataset"></a>Erstellen eines Datasets

Da Sie nun über einige Computeressourcen verfügen, die Sie zum Verarbeiten von Daten verwenden können, benötigen Sie eine Möglichkeit, die zu verarbeitenden Daten zu speichern und zu erfassen.

1. Zeigen Sie die durch Trennzeichen getrennten Daten unter https://aka.ms/diabetes-data in Ihrem Webbrowser an. Speichern Sie diese dann als lokale Datei namens **diabetes.csv** (der Speicherort spielt keine Rolle).
2. Zeigen Sie in Azure Machine Learning Studio die Seite **Datasets** an. Datasets stellen bestimmte Datendateien oder Tabellen dar, mit denen Sie in Azure Machine Learning arbeiten möchten.
3. Erstellen Sie mithilfe der folgenden Einstellungen ein neues Dataset aus lokalen Dateien:
    * **Basisinformationen:**
        * **Name**: Diabetes-Dataset
        * **Datasettyp:** Tabellarisch
        * **Beschreibung:** Diabetesdaten
    * **Datastore and file selection** (Datenspeicher und Dateiauswahl):
        * **Select or create a datastore** (Datenspeicher auswählen oder erstellen): Aktuell ausgewählter Datenspeicher
        * **Dateien für Dataset auswählen**: Navigieren Sie zur heruntergeladenen Datei **diabetes.csv**.
        * **Uploadpfad**: *Übernehmen Sie die Standardauswahl.*
        * **Skip data validation** (Datenüberprüfung überspringen): Nicht ausgewählt
    * **Einstellungen und Vorschau:**
        * **Dateiformat:** Zeichengetrennt
        * **Trennzeichen:** Komma
        * **Codierung:** UTF-8
        * **Spaltenüberschriften**: Nur erste Datei enthält Header
        * **Zeilen überspringen:** Keine
    * **Schema:**
        * Alle Spalten einschließen außer **Pfad**
        * Überprüfen der automatisch erkannten Typen
    * **Details bestätigen:**
        * Nach der Erstellung kein Profil für dieses Dataset erstellen
4. Nachdem das Dataset erstellt wurde, öffnen Sie es, und zeigen Sie die Seite **Erkunden** an, um eine Stichprobe der Daten anzuzeigen. Diese Daten repräsentieren detaillierte Angaben zu Patienten, die auf Diabetes getestet wurden. Mithilfe dieser Daten werden Sie ein Modell trainieren, das auf der Grundlage klinischer Messungen die Wahrscheinlichkeit vorhersagt, dass ein Patient positiv auf Diabetes getestet wird.

    > **Hinweis**: Sie können optional ein *Profil* des Datasets generieren, um weitere statistische Details anzuzeigen.

## <a name="run-an-automated-machine-learning-experiment"></a>Ausführen eines automatisierten Machine Learning-Experiments

In Azure Machine Learning werden ausgeführte Vorgänge *Experimente* genannt. Führen Sie die folgenden Schritte aus, um ein Experiment auszuführen, das das automatisierte maschinelle Lernen zum Trainieren eines Klassifizierungsmodells verwendet, das Diabetesdiagnosen vorhersagt.

1. Zeigen Sie in Azure Machine Learning Studio die Seite **Automatisiertes ML** (unter **Autor**) an.
2. Erstellen Sie eine neue automatisierte ML-Ausführung mit den folgenden Einstellungen:
    - **Dataset auswählen:**
        - **Dataset**: Diabetes-Dataset
    - **Konfigurieren der Ausführung:**
        - **Name des neuen Experiments**: mslearn-automl-diabetes
        - **Zielspalte**: Diabetiker (*Dies ist die Beschriftung, die das Modell durch das Training vorhersagen soll.* )
        - **Computetyp auswählen**: Computecluster
        - **Azure ML-Computecluster auswählen**: *zuvor erstellter Computecluster*
    - **Tasktyp- und einstellungen**:
        - **Aufgabentyp**: Klassifizierung
        - Wählen Sie **Zusätzliche Konfigurationseinstellungen anzeigen** aus, um **Zusätzliche Konfigurationen** zu öffnen:
            - **Primary metric** (Primäre Metrik): Wählen Sie **AUC_Weighted** aus (*Weitere Informationen zu dieser Metrik folgen später.* )
            - **Explain best model** (Bestes Modell erklären): ausgewählt – *Diese Option bewirkt, dass mit dem automatisierten maschinellen Lernen die Relevanz der Merkmale für das beste Modell berechnet wird. So können Sie den Einfluss der einzelnen Merkmale auf die vorhergesagte Bezeichnung ermitteln.*
            - **Alle unterstützten Modelle verwenden**: <u>Nicht</u> ausgewählt: Sie beschränken das Experiment darauf, einige bestimmte Algorithmen auszuprobieren.
            - **Zulässige Modelle**: Wählen Sie nur **LogisticRegression** und **RandomForest** aus. Dies sind die einzigen Algorithmen, die im Experiment getestet werden.
            - **Exit criterion** (Beendigungskriterien):
                - **Trainingsauftragszeit (Stunden)**: 0,5 – *Dies bewirkt, dass das Experiment nach maximal 30 Minuten beendet wird.*
                - **Metrischer Bewertungsschwellenwert**: 0,90 – *Dies führt dazu, dass das Experiment beendet wird, wenn ein Modell eine gewichtete AUC-Metrik von 90 % oder höher erreicht.*
        - Wählen Sie **Featurisierungseinstellungen anzeigen** aus, um die **Featurisierung** zu öffnen:
            - **Enable featurization** (Featurisierung aktivieren): ausgewählt – *Dies bewirkt, dass Azure Machine Learning die Merkmale vor dem Training automatisch vorverarbeitet*.
    - **Validierungs- und Testtyp auswählen**:
        - **Validierungstyp**: Aufteilung der Train-Validation
        - **Prozentsatz der Datenvalidierung**: 30
        - **Testdataset**: Kein Testdataset erforderlich

3. Wenn Sie die Details für die automatisierte ML-Ausführung übermittelt haben, wird der Vorgang automatisch gestartet. Sie können den Status der Ausführung im Bereich **Eigenschaften** beobachten.
4. Wenn der Status der Ausführung in *Wird ausgeführt* geändert wird, zeigen Sie die Registerkarte **Modelle** an, und achten Sie darauf, dass jede mögliche Kombination aus Trainingsalgorithmen und Vorverarbeitungsschritten ausprobiert und die Leistung des resultierenden Modells ausgewertet wird. Die Seite wird automatisch regelmäßig aktualisiert, aber Sie können auch auf **&#8635; Aktualisieren** klicken. Es kann etwa zehn Minuten dauern, bis die Modelle angezeigt werden, weil die Clusterknoten initialisiert werden müssen und der Datenfeaturisierungsprozess abgeschlossen sein muss, bevor das Training beginnen kann. Jetzt ist vielleicht ein guter Zeitpunkt für eine Kaffeepause!
5. Warten Sie, bis das Experiment abgeschlossen ist.

## <a name="review-the-best-model"></a>Überprüfen des besten Modells

Nachdem das Experiment abgeschlossen wurde, können Sie das generierte Modell mit der besten Leistung überprüfen. (Beachten Sie, dass in diesem Fall Beendigungskriterien verwendet wurden, um das Experiment zu beenden. Daher ist das im Rahmen des Experiments ermittelte „beste“ Modell möglicherweise nicht das bestmögliche Modell, sondern nur das beste, das innerhalb der für diese Übung festgelegten Zeit- und Metrikeinschränkungen gefunden wurde.)

1. Beachten Sie auf der Registerkarte **Übersicht** der automatisierten ML-Ausführung die Zusammenfassung des besten Modells.
2. Wählen Sie den **Algorithmusnamen** für das beste Modell aus, um die untergeordnete Ausführung anzuzeigen, durch die es generiert wurde.

    Das beste Modell wird basierend auf der von Ihnen angegebenen Auswertungsmetrik identifiziert (*AUC_Weighted*). Im Rahmen des Trainingsprozesses wurden zum Berechnen dieser Metrik einige Daten für das Modelltraining verwendet. Außerdem wurde eine Technik namens *Kreuzvalidierung* angewendet, um das trainierte Modell iterativ mit Daten zu testen, mit denen es nicht trainiert wurde, und den vorhergesagten Wert mit dem tatsächlichen bekannten Wert zu vergleichen. Aus diesen Vergleichen wird eine *Konfusionsmatrix* aus „true-positives“, „false-positives“, „true-negatives“ und „false-negatives“ zusammengestellt, und es werden zusätzliche Klassifizierungsmetriken berechnet, einschließlich eines Diagramms mit einer ROC-Kurve (Receiver Operating Characteristics), in dem die True-Positive-Rate mit der False-Positive-Rate verglichen wird. Die Fläche unter der Kurve (Area Under the Curve, AUC) ist eine allgemeine Metrik, die zum Auswerten der Klassifizierungsleistung verwendet wird.
3. Klicken Sie neben dem Wert *AUC_Weighted* auf **Alle weiteren Metriken anzeigen**, um Werte anderer möglicher Auswertungsmetriken für ein Klassifizierungsmodell anzuzeigen.
4. Wählen Sie die Registerkarte **Metriken** aus, und überprüfen Sie die Leistungsmetriken, die Sie für das Modell anzeigen können. Dazu gehören eine Visualisierung **confusion_matrix**, die die Konfusionsmatrix für das validierte Modell zeigt, und eine Visualisierung **accuracy_table**, die das ROC-Diagramm enthält.
5. Wählen Sie die Registerkarte **Erklärungen** aus, wählen Sie eine **Erklärungs-ID** aus, und zeigen Sie dann die Seite **Aggregierte Wichtigkeit** an. Diese zeigt an, wie stark sich die einzelnen Merkmale im Dataset auf die Beschriftungsvorhersage auswirken.

## <a name="deploy-a-predictive-service"></a>Bereitstellen eines Vorhersagediensts

Nachdem Sie mithilfe von automatisiertem maschinellem Lernen einige Modelle trainiert haben, können Sie das Modell mit der besten Leistung als Dienst bereitstellen, das dann von Clientanwendungen verwendet werden kann.

> **Hinweis**: In Azure Machine Learning können Sie einen Dienst als ACI-Instanz (Azure Container Instances) oder in einem AKS-Cluster (Azure Kubernetes Service) bereitstellen. In Produktionsszenarios wird eine AKS-Bereitstellung empfohlen, für die Sie einen *Rückschlusscluster* als Computeziel erstellen müssen. In dieser Übung verwenden Sie einen ACI-Dienst, der ein geeignetes Bereitstellungsziel für Tests darstellt. Es ist nicht erforderlich, einen Rückschlusscluster zu erstellen.

1. Wählen Sie die Registerkarte **Übersicht** für die Ausführung aus, die das beste Modell erzeugt hat.
2. Verwenden Sie in der Option **Bereitstellen** die Schaltfläche **Für Webdienst bereitstellen**, um das Modell mit den folgenden Einstellungen bereitzustellen:
    - **Name**: auto-predict-diabetes
    - **Beschreibung**: Vorhersage von Diabetes
    - **Computetyp:** Azure Container Instances
    - **Authentifizierung aktivieren:** ausgewählt
    - **Benutzerdefinierte Bereitstellungsressourcen verwenden**: Nicht ausgewählt
3. Warten Sie, bis die Bereitstellung gestartet wurde. Dieser Vorgang kann einige Sekunden in Anspruch nehmen. Beachten Sie dann auf der Registerkarte **Modell** im Abschnitt **Modellzusammenfassung** den **Bereitstellungsstatus** für den Dienst **auto-predict-diabetes**, der **Wird ausgeführt** lauten sollte. Warten Sie, bis der Status in **Erfolgreich** geändert wurde. Möglicherweise müssen Sie in regelmäßigen Abständen auf **&#8635; Aktualisieren** klicken.  **HINWEIS** Dies kann eine Weile dauern – wir bitten um Geduld.
4. Zeigen Sie in Azure Machine Learning Studio die Seite **Endpunkte** an, und wählen Sie den Echtzeitendpunkt für **auto-predict-diabetes** aus. Klicken Sie dann auf die Registerkarte **Consume** (Nutzen), und notieren Sie sich die folgenden Informationen. Sie benötigen diese Informationen, um von einer Clientanwendung aus eine Verbindung mit dem bereitgestellten Dienst herzustellen.
    - REST-Endpunkt für Ihren Dienst
    - Primärschlüssel für Ihren Dienst
5. Beachten Sie, dass Sie den Link &#10697; neben diesen Werten verwenden können, um diese in die Zwischenablage zu kopieren.

## <a name="test-the-deployed-service"></a>Testen des bereitgestellten Diensts

Nachdem Sie nun einen Dienst bereitgestellt haben, können Sie ihn mithilfe von einfachem Code testen.

1. Lassen Sie die Seite **Nutzen** für die Seite des Diensts **auto-predict-diabetes** in Ihrem Browser geöffnet, und öffnen Sie eine neue Browserregisterkarte sowie eine zweite Instanz von Azure Machine Learning Studio. Zeigen Sie dann auf der neuen Registerkarte die Seite **Notebooks** an.
2. Navigieren Sie auf der Seite **Notebooks** unter **Meine Dateien** zum Ordner **/users/*Ihr-Benutzername*/mslearn-dp100**, in den Sie das Repository für Notebooks geklont haben, und öffnen Sie das Notebook **Get AutoML Prediction** (AutoML-Vorhersage abrufen).
3. Nachdem das Notebook geöffnet wurde, vergewissern Sie sich, dass die zuvor erstellte Compute-Instanz im Feld **Compute** ausgewählt ist und dass sie den Status **Wird ausgeführt** aufweist.
4. Ersetzen Sie im Notebook die Platzhalter **ENDPOINT** und **PRIMARY_KEY** durch die Werte für Ihren Dienst, die Sie von der Registerkarte **Nutzen** auf der Seite für Ihren Endpunkt kopieren können.
5. Führen Sie die Codezelle aus, und zeigen Sie die von Ihrem Webdienst zurückgegebene Ausgabe an.

## <a name="clean-up"></a>Bereinigung

Der von Ihnen erstellte Webdienst wird in einer *Azure-Containerinstanz* gehostet. Wenn Sie nicht weiter experimentieren möchten, sollten Sie den Endpunkt löschen, um eine unnötige Azure-Nutzung zu vermeiden. Sie sollten auch die Compute-Instanz beenden, bis Sie sie wieder benötigen.

1. Wählen Sie in Azure Machine Learning Studio auf der Registerkarte **Endpunkte** den Endpunkt **auto-predict-diabetes** aus. Klicken Sie dann auf **Löschen** (&#128465;), und bestätigen Sie, dass Sie den Endpunkt löschen möchten.
2. Wählen Sie auf der Seite **Compute** auf der Registerkarte **Compute-Instanzen** Ihre Compute-Instanz und dann **Beenden** aus.

> **Hinweis**: Durch das Beenden Ihrer Compute-Instanz wird sichergestellt, dass Ihrem Abonnement keine Computeressourcen in Rechnung gestellt werden. Ihnen wird jedoch eine geringe Datenspeichermenge in Rechnung gestellt, solange der Azure Machine Learning-Arbeitsbereich in Ihrem Abonnement enthalten ist. Wenn Sie mit dem Erkunden von Azure Machine Learning fertig sind, können Sie Ihren Azure Machine Learning-Arbeitsbereich und die zugehörigen Ressourcen löschen. Wenn Sie jedoch weitere Labs in dieser Reihe durchführen möchten, müssen Sie die Übung *[Erstellen eines Azure Machine Learning-Arbeitsbereichs](01-create-a-workspace.md)* wiederholen, um zunächst den Arbeitsbereich zu erstellen und die Umgebung vorzubereiten.
