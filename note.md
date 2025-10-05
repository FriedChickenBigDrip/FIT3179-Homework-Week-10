https://www.bom.gov.au/cyclone/tropical-cyclone-knowledge-centre/databases/

          "scale": {
            "type": "threshold",
            "domain": [17067, 20367, 23667, 26967, 30267, 33567, 36867],
            "range": ["#fee5d9", "#fcae91", "#fb6a4a", "#e6550d", "#a63603", "#7f2704"]
          },




          {
      "data": {
        "url": "data/VictMedianSalaryPerJob.csv"
      },
      "transform": [
        {
          "filter": "datum.Sup_Time_Period == Year_selection"
        },
        {
          "window": [{"op": "rank", "as": "ranking"}],
          "sort": [{"field": "ChangePerc", "order": "descending"}]
        },
        {"filter": "datum.ranking == 1"},
        {
          "calculate": "'Highest % Change:; ' + datum['ChangePerc']",
          "as": "text_annotation_raw"
        },
        {
          "calculate": "split(datum.text_annotation_raw, ';')",
          "as": "text_annotation"
        }
      ],
      "mark": {
        "type": "text",
        "align": "right",
        "dx": 0,
        "dy": 0,
        "baseline": "middle",
        "fontStyle": "italic"
      },
      "encoding": {"text": {"field": "text_annotation"}}
    }