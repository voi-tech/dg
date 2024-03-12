---
{"dg-publish":true,"permalink":"/weblog/my-daily-note-template-2024/"}
---


# My Daily Note Template 2024

Szablon notatki codziennej, czyli takiej, której tytuł to dzisiejsza data a treść odnosi się do dzisiejszego dnia.

Wymagane wtyczki:

- Templater
- Daily Notes
- Dataview

````

# <% tp.date.now("dddd, DD MMMM YYYY") %>

<% tp.web.daily_quote() %>

## Daily Log

- tutaj wpisuję wydarzenia z dzisiejszego dnia z godziną

## Notes


{ .block-language-dataview}
````

Nazwa notatki to dzisiejsza data w formacie `YYYY-MM-DD`, czyli np. `2024-03-15`.

Tytuł notatki jest zapisany jako nagłówek pierwszego poziomu, czyli H1:

`# <% moment(tp.file.title,'YYYY-MM-DD').format("dddd, DD MMMM YYYY") %>`

Templater wykrywa datę na podstawie nazwy notatki i zamienia na format `"dddd, DD MMMM YYYY"`, czyli np. `Friday, 15 March 2024`. 

Poniżej znajduje się losowy cytat: `<% tp.web.daily_quote() %>`, który automatycznie dostosowuje format.

Następna sekcja to `## Daily Log`, czyli wydarzenia w ciągu dnia. Wpisuję je ręcznie lub korzystam ze skrótu w aplikacji Apple Shortcuts, który wyciąga dane z aplikacji Apple Calendar (Kalendarz) i Apple Reminders (Przypomnienia) i dodaje pod tym nagłówkiem w kolejności chronologicznej.

Ostatnia sekcja to `## Notes`, czyli zbiór notatek utworzonych lub zmodyfikowanych dzisiaj. Notatki są automatycznie dodawane za pomocą wtyczki Dataview, ale nic nie stoi na przeszkodzie, aby robić to ręcznie.

````

{ .block-language-dataview}
````

Powyższy skrypt tworzy listę notatek (`list`), gdzie nazwa pliku to nie jest nazwa tego pliku (`where file.name != this.file.name`), czyli ta notatka codzienna nie wyświetli się na tej liście. I dodatkowo dzień ostatniej modyfikacji pliku jest taki sam, jak dzień utworzenia tej notatki (`and file.mday = this.file.day`). Lista jest sortowana chronologicznie w odwróconej kolejności, czyli pliki ostatnio edytowane będą na samej górze (`sort file.mtime desc`).

Dodatkowo poniżej dodaję wszystkie inne rzeczy, typu linki do stron internetowych, które dziś znalazłem i chciałbym zachować.

W ustawieniach wtyczki nazwa notatki jest zdefiniowana w taki sposób, aby automatycznie tworzyć notatkę w dedykowanym folderze. Format wygląda następująco: `YYYY/MM-MMMM/YYYY-MM-DD`, czyli notatka o nazwie `2024-03-15` jest w folderze `03-March`, który jest w folderze `2024`.
