# ARES
 ИИ нового поколения, названный в честь бога войны, чтобы побеждать рутину. Он превращает массивные потоки информации в ваше главное конкурентное преимущество
import random
import datetime
from typing import List, Dict, Optional

class AresAI:
    def __init__(self, name: str = "ARES"):
        self.name = name
        # Используем словарь для быстрого поиска ответов (Ключ: Вопрос, Значение: Ответ)
        self.brain: Dict[str, str] = {}
        self.history: List[str] = []

    def _normalize(self, text: str) -> str:
        """Внутренний метод для очистки входных данных."""
        return text.strip().lower()

    def learn(self, query: str, answer: str) -> None:
        """Метод обучения: связывает запрос с конкретным знанием."""
        normalized_query = self._normalize(query)
        self.brain[normalized_query] = answer
        print(f"[{self.name}]: Знание усвоено -> '{query}'")

    def respond(self, query: str) -> str:
        """Логика принятия решения и поиска ответа."""
        normalized_query = self._normalize(query)
        
        # 1. Проверка в базе знаний
        if normalized_query in self.brain:
            response = f"Анализ завершен: {self.brain[normalized_query]}"
        else:
            # 2. Если не знает — генерирует творческий ответ
            response = self._generate_creative_response()
            
        self.history.append(f"Q: {query} | A: {response}")
        return response

    def _generate_creative_response(self) -> str:
        """Творческая заглушка для неизвестных данных."""
        scenarios = [
            "Данных недостаточно для точного прогноза. Требуется дообучение.",
            "Этот запрос выходит за рамки текущей стратегии. Изучить подробнее?",
            "Интересный паттерн. Мои алгоритмы пока не нашли совпадений.",
            "Для победы над этой задачей мне нужно больше контекста."
        ]
        return random.choice(scenarios)

    def select_strategy(self, options: List[str]) -> str:
        """Принятие решения на основе взвешенного выбора (имитация стратегии)."""
        decision = random.choice(options)
        return f"Выбрана оптимальная стратегия: {decision}"

    def show_stats(self):
        """Вывод состояния системы."""
        print(f"\n--- Статус {self.name} ---")
        print(f"Объем базы знаний: {len(self.brain)} записей")
        print(f"Обработано запросов: {len(self.history)}")
        print("------------------------\n")

# --- Боевое крещение ARES ---
ares = AresAI()

# Обучаем конкретным фактам
ares.learn(
    "Какая главная цель?", 
    "Превращать хаос информации в стратегическое преимущество."
)
ares.learn(
    "Что такое ИИ?", 
    "Это инструмент эволюции разума."
)

# Тестируем интеллект
print(f"ARES: {ares.respond('КАКАЯ ГЛАВНАЯ ЦЕЛЬ?')}") # Сработает нормализация
print(f"ARES: {ares.respond('Как мне захватить рынок?')}") # Неизвестный вопрос
print(f"ARES: {ares.select_strategy(['Агрессивный рост', 'Удержание позиций', 'Масштабирование'])}")

ares.show_stats()
