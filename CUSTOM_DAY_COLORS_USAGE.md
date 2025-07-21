# Custom Day Column Colors Usage

## Опис
Цей патч додає можливість кастомізувати колір стовпчиків днів у Gantt діаграмі через новий проп `getDayColumnColor`.

## Використання

```tsx
import React from 'react';
import { Gantt, Task } from 'gantt-task-react';

const tasks: Task[] = [
  // ваші задачі...
];

// Функція для визначення кольору стовпчика дня
const getDayColumnColor = (date: Date): string | undefined => {
  const dayOfWeek = date.getDay();
  
  // Вихідні дні - світло-сірий фон
  if (dayOfWeek === 0 || dayOfWeek === 6) {
    return 'rgba(200, 200, 200, 0.3)';
  }
  
  // Активні дні (понеділок-п'ятниця) - світло-зелений фон
  return 'rgba(144, 238, 144, 0.2)';
};

const MyGanttChart = () => {
  return (
    <Gantt
      tasks={tasks}
      getDayColumnColor={getDayColumnColor}
      // інші пропси...
    />
  );
};
```

## Інші приклади

### Виділення святкових днів
```tsx
const holidays = new Set([
  '2024-01-01', // Новий рік
  '2024-12-25', // Різдво
  // інші свята...
]);

const getDayColumnColor = (date: Date): string | undefined => {
  const dateString = date.toISOString().split('T')[0];
  
  if (holidays.has(dateString)) {
    return 'rgba(255, 99, 132, 0.3)'; // Червоний для свят
  }
  
  return undefined; // Стандартний колір
};
```

### Виділення робочих/неробочих днів
```tsx
const getDayColumnColor = (date: Date): string | undefined => {
  const dayOfWeek = date.getDay();
  
  // Вихідні - червонуватий
  if (dayOfWeek === 0 || dayOfWeek === 6) {
    return 'rgba(255, 0, 0, 0.1)';
  }
  
  // Робочі дні - зеленуватий
  return 'rgba(0, 255, 0, 0.1)';
};
```

## Примітки
- Функція `getDayColumnColor` викликається для кожного дня в календарі
- Поверніть `undefined` або `null`, щоб використати стандартний колір
- Використовуйте прозорі кольори (rgba) для кращого візуального ефекту
- Кастомні кольори рендеряться під стовпчиком "сьогодні" (today)