<!-- --------------FONT-LINK------------ -->

<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=Titan+One&display=swap"
     rel="stylesheet">

<!-- -----------FONT-ROOTS--------- -->

:root {
--primary-font: "DM Sans", sans-serif;
--titan-font: "Titan One", cursive;
}

<!-- ------------BODY------------ -->

body {
font-family: var(--primary-font);
font-weight: 500;
font-size: 12px;

@media screen and (min-width: 700px) and (max-width: 1049px) {
font-size: 14px;
}

@media screen and (min-width: 1050px) {
font-size: 16px;
}
}

<!-- Функция и миксин для шрифта -->

// Функция нужна, чтобы округлить line-height до трёх цифр после точки

@function decimal-round($number, $digits: 0, $mode: round) {
  $n: 1;
  // $number must be a number
  @if type-of($number) != number {
@warn '#{ $number } is not a number.';
    @return $number;
  }
  // $digits must be a unitless number
  @if type-of($digits) != number {
@warn '#{ $digits } is not a number.';
    @return $number;
  } @else if not unitless($digits) {
@warn '#{ $digits } has a unit.';
    @return $number;
  }
  @if $digits > 0 {
    @for $i from 1 through $digits {
      $n: $n * 10;
    }
  }
  @if $mode == round {
    @return round($number _ $n) / $n;
  } @else if $mode == ceil {
    @return ceil($number _ $n) / $n;
  } @else if $mode == floor {
    @return floor($number \* $n) / $n;
} @else {
@warn '#{ $mode } is undefined keyword.';
@return $number;
}
}

// ---FONT-MIXIN---

@mixin font($fw, $fs, $lh) {
  font-weight: $fw;
  font-size: $fs;
  line-height: decimal-round($lh/$fs, 3);
}

// чтобы использовать миксин в стилях, пишем @include font();
// где в скобках в обязательной очередности указать через запятую font-weight, font-size, line-height как на макете
// Последние два с пикселями.
// Line-height пересчитывать не нужно - миксин с подключенной функцией делит автоматом
