## C3 — компонентные диаграммы (4 файла)
Детализированы два наиболее интересных контейнера в каждом решении — Video Analytics и Event Engine, так как именно в них сосредоточена вся критическая бизнес-логика.
Решение 1 (s1): Video Analytics публикует события через gRPC напрямую в Event Engine. Внутри агента 8 компонентов: от Stream Manager до gRPC Server.
Решение 2 (s2): Video Analytics Node публикует через NATS JetStream с параллельной персистентностью в локальную БД. Event Node добавляет NATS Consumer и Sync Agent как отдельные компоненты.


## C4 — диаграммы кода (4 файла)
Для решения 1 сгенерированы ключевые классы с полями, методами и отношениями:
c4-code-s1-event-classifier — Python-классы EventClassifier, иерархия правил (FightDetectionRule, PigletCrushingRule, IllnessRule), value objects Detection и DetectionEvent.
c4-code-s1-rule-engine — Go-классы RuleEngine с композицией правил (ThresholdRule, TimeWindowRule, CompositeRule), контекст истории событий, конфигурация через YAML.