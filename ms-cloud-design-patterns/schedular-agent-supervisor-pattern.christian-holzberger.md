# Scheduler Agent Supervisor Pattern

Das Pattern dient dazu Aufgaben in der Cloud auszuf�hren und zu Koordinieren. 
Cloud bedeutet dabei, dass mehrere Systeme am ausf�hren von Aufgaben beteiligt werden.
Durch den Einsatz des Patterns soll vorallem im Fehlerfall, beim Absturz des Supervisors 
oder beim Fehlschalgen einzelner Aktionen, ein definierter Zustand wiederhergestellt wird (Self-Healing). 

Eine Aufgabe wird definiert durch eine Remote URL, einen Timeout. ... tbd

Das Pattern beinhaltet 3 Zust�ndigkeiten: 
- Scheduler
- Agent 
- Supervisor 

Durch den Scheduler wird die Reihenfolge der Ausf�hrung der Aufgaben festgelegt. Weiterhin wird der derzeige Zustand der Aufgabe festgehalten, 
welche Teilschritte ausgef�hrt wurden und in welchem Zustand sich die derzeitige Teilaufgabe befindet. Der Superviros speichert den Zustand der aktuellen Ausf�hrung in 
einer Datenbank dem "State-Store".
... was passiert beim Absturz

Der Agent koordiniert den Aufruf der konkreten Aufgabe. Er Pr�ft den Zustand einer Aufgabe und kann den Scheduler anweisen bestimmte Aktionen erneut auszuf�hren. 
Er entspricht im wesentlichen dem Proxy-Pattern mit der Erweiterung von Timeouts und kommunikation mit einem bekannten Scheduler. Der Agent ist m�glich generisch zu halten 
er sollte keine Kentniss des aktuellen Gesch�ftsvorgangs haben.

Der Supervisor benutzt den Agent um den Status einer Teilaufgabe abzufragen und dem Scheduler zug�nglich zu machen. 

Im Kontext von Cloud-Anwendungen ist die Koordinierung der Aufgaben besonders wichtig, insbesondere ist es wichtig, dass Aufgaben nicht mehrfach Ausgef�hrt werden. Um dies Sicherzustellen muss zus�tzlich 
zum Scheduler Agent Supervisor Pattern auf das Leader Election Pattern zur�ckgegriffen werden. Pro Aufgabe muss ein Scheduler ausgemacht werden der f�r diese spezifische Aufgabe verantwortlich ist. 


