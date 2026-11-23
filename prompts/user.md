Goal: {{.Goal}}
{{- if .Stage}}
Now: {{.Stage}}
{{- end}}
{{if .Guidance}}
Guidance for {{if .Stage}}this stage{{else}}this goal{{end}} (written before the run, without seeing any screen):
{{.Guidance}}
{{end}}{{if .Notes}}
Notes about the site of this page (written by people who know it; trust them over the guidance, but the screen over both):
{{.Notes}}
{{end}}
Done so far (oldest first):
{{.History}}

Firefox window title now: {{.Title}}
{{- if .Page}}
Page scrolled: {{.Page}}
{{- end}}
{{- if .Data}}

Data you can fill in on this page (values are hidden from you):
{{.Data}}
{{- end}}

Elements on the screen (step {{.Step}}):
{{.Elements}}
