# Graph-modal

Простая и легкая JavaScript-библиотека для модальных окон

## Особенности

+ __Никаких зависимостей__.  Библиотека написана на чистом JavaScript, для работы не требуются иные библиотеки.
+ __Простота и функциональность__. Вы можете легко и быстро подключить и использовать библиотеку, которая реализует важный функционал для модальных окон: отключение скролла, разные способы закрытия окна, центрирование окна и т.д.
+ __Фокусируемость__. При открытии окна фокус фиксируется внутри него.
+ __Настройка с помощью CSS__. Вы можете легко менять внешний вид, расположение и даже анимацию появления с помощью CSS.
+ __Окно из окна__. Библиотека позволяет открыть новое окно из другого окна (при этом предыдущее закроется).

## Как работать с библиотекой

1. Скачайте последнюю версию библиотеки
2. Подключите graph-modal.min.css и graph-modal.min.js из папки dist к странице
3. Поместите в ваш html-документ следующую разметку:
```html
<div class="graph-modal">
	<div class="graph-modal__container" role="dialog" aria-modal="true" data-graph-target="first">
		<button class="btn-reset graph-modal__close" aria-label="Закрыть модальное окно"></button>
		<div class="graph-modal__content">
			<!-- контент модального окна -->
		</div>
	</div>
</div>
```
### Важные нюансы селекторов

`.graph-modal` - Элемент окна-родителя для других модальных окон, то есть в него вкладываются все модальные окна на сайте, которые вам нужны. Также является "затемнением" сайта при открытии окна.

`.graph-modal__container` - Элемент самого модального окна. Имеет атрибут `[data-graph-target]`, предназначенный для связи с открывающей кнопкой.

`.js-modal-close` - Элемент, закрывающий текущее модальное окно.

4. Разместите следующий JS-код для подключения модального окна:

```javascript
const modal = new GraphModal();
```
5. Создайте в разметке кнопку, которая будет открывать модальное окно. Задайте ей атрибут `[data-graph-path]` со значением, равным значению `[data-graph-target]` у модального окна.

## Открытие конкретного окна по событию

Вы можете сразу открыть окно, если создадите экземпляр класса и сразу вызовите у него метод `open()` с передачей значения атрибута `[data-graph-target]`. Пример:

```javascript
document.querySelector('.btn').addEventListener('click', () => {
	new GraphModal().open('second');
});
```

## Настройки
Настраивать модальное окно можно исключительно через html-разметку:
1. Для определения анимации модального окна добавьте элементу, открывающему модальное окно, атрибут `[data-graph-animation=""]` с нужным вам значением (по умолчанию fade).
По умолчанию доступны два варианта анимации - `fade` и `fadeInUp`, однако вы можете написать любое значение атрибута, а затем определить его в css-стилях. Пример:
```html
<button class="btn-reset modal-btn" data-graph-animation="custom" data-graph-path="second">Открыть окно</button>
```

```css
.custom.animate-open {
	opacity: 1;
	transform: rotate(180deg);
	transition: transform var(--transition-time), opacity var(--transition-time);
}
```

Таким образом вы осуществляете привязку атрибута `custom` и класса `.custom`

2. Для определения времени анимации появления окна добавьте элементу, открывающему модальное окно, атрибут `[data-graph-speed=""]` с нужным вам значением (по умолчанию 300мс). Поскольку плагин использует Css Custom Properties (css-переменные), таким образом вы сможете переназначить переменную `--transition-time` в нужном месте. Пример:

```html
<button class="btn-reset modal-btn" data-graph-animation="custom" data-graph-path="second" data-graph-speed="500">Открыть окно</button>
```

## События

Библиотека поддерживает два события:

1. Событие `isOpen` - срабатывает в момент открытия модального окна. Может принимать входной параметр - объект открытого окна, например, для помещения в модальное окно чего-либо через js. Пример:

```javascript
const modal = new GraphModal({
	isOpen: (modal) => {
		console.log(modal);
		console.log('opened');
	},
});
```

2. Событие `isClose` - срабатывает в момент закрытия модального окна. Пример:

```javascript
const modal = new GraphModal({
	isOpen: (modal) => {
		console.log(modal);
		console.log('opened');
	},
	isClose: () => {
		console.log('closed');
	}
});
```

Пример работы библиотеки вы можете увидеть, открыв файл index.html в браузере.

Приятного пользования!
