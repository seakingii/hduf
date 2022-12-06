> 此仓库中 clone 于 https://github.com/muesli/duf
> 主要做了一些修改,供其它包调用(不然的话是一个 program 包,不能调用)

调用例子如下:

```
console := types.NewConsoleBuilder()

	m, warnings, err := hduf.Mounts()

	if err != nil {
		console.Red(err.Error()).Println()
		return
	}

	if len(warnings) > 0 {
		for _, warning := range warnings {
			console.Yellow(warning).Println()
		}
	}

	var width uint = 0

	isTerminal := term.IsTerminal(int(os.Stdout.Fd()))
	if isTerminal && width == 0 {
		w, _, err := term.GetSize(int(os.Stdout.Fd()))
		if err == nil {
			width = uint(w)
		}
	}

	hduf.SetAnsiTheme()
	hduf.SetWidth(width)

	filters := hduf.FilterOptions{}

	hduf.RenderTables(m, filters, hduf.TableOptions{
		Columns: []int{1, 2, 3, 4, 5, 10, 11},
		SortBy:  0,
		Style:   table.StyleDefault,
	})
```