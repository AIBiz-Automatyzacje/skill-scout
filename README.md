# Skill Scout 🔍

Skaut Twojej własnej pracy dla Claude Code. Czyta logi sesji, wykrywa **powtarzalną ręczną robotę** (te same prośby ≥3× w oknie czasowym) i podaje gotową listę procesów, które warto opakować w skill — posortowaną po zwrocie z czasu.

Bliźniak `reflect` / `memory-update` (ten sam wzorzec: logi sesji → sygnały → wynik), ale zamiast kalibrować osobowość czy stan projektów, szuka **żmudnych procesów do automatyzacji**.

**Zasada nadrzędna:** scout niczego nie buduje i nie zmienia — tylko czyta logi i pisze raport HTML + plik stanu. Decyzję, co faktycznie opakować w skill, podejmujesz Ty.

## Jak działa

1. Parsuje Twoje prośby z logów sesji Claude Code (`~/.claude/projects/`) w oknie N dni.
2. Grupuje je w procesy (intencja, nie dosłowne zdania) i wyłapuje te powtarzane **≥3×**.
3. Liczy potencjał oszczędności (`freq × minut na przebieg`) i sortuje malejąco.
4. Generuje raport HTML z kandydatami: nowe na górze, wcześniej wytypowane poniżej.
5. Pamięta co już zgłosił (`_proposed.json`) — polityka „zaproponuj raz, nigdy więcej".

## Instalacja

Skill jest pojedynczym skillem Claude Code. Sklonuj go do katalogu skilli:

```bash
git clone https://github.com/AIBiz-Automatyzacje/skill-scout.git ~/.claude/skills/skill-scout
```

Albo do skilli konkretnego projektu (`<projekt>/.claude/skills/skill-scout`).

## Użycie

```
/skill-scout            # okno 7 dni (domyślnie)
/skill-scout 14         # 14 / 21 / 30 dni — audyt szerszego okna
```

Frazy wyzwalające: „skill scout", „co warto opakować w skill", „przegląd powtarzalnej roboty", „co zautomatyzować".

## Wymagania

- **Claude Code** z logami sesji w `~/.claude/projects/`
- **Python 3** (parser) i **Node.js** (generator raportu HTML)
- Ścieżki wyjściowe (`Zasoby/skill-scout/`) są dopasowane pod vault Obsidian — dostosuj pod swój setup, jeśli używasz innej struktury.

## Pliki

| Plik | Rola |
|------|------|
| `SKILL.md` | Definicja skilla — pełny pipeline 9 kroków |
| `scripts/parse_intents.py` | Ekstrakcja próśb użytkownika z logów sesji |
| `scripts/generate-raport.mjs` | Generator raportu HTML |
| `evals/evals.json` | Zestaw ewaluacyjny |

---

Część kursu **Osobisty Asystent AI** — [Akademia Automatyzacji](https://akademiaautomatyzacji.com).
