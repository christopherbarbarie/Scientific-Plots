# Scientific-Plots
Changes the default style in matplotlib and an agentic skill file with some rules for making plots.

Adapted from Ciaran O'Hare's talk "How to make a plot"
([github.com/cajohare/HowToMakeAPlot](https://github.com/cajohare/HowToMakeAPlot)),
with some personal opinions added on.

- `paper.mplstyle`: the matplotlib style. Use it with `plt.style.use('path/to/paper.mplstyle')`,
  or copy it into `matplotlib.get_configdir()/stylelib/` and use `plt.style.use('paper')`.
- `skills/scientific-plots/SKILL.md`: the skill. Copy the folder into `~/.claude/skills/`
  for Claude Code, or upload it as a skill on claude.ai.
