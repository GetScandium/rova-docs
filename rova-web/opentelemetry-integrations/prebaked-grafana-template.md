# PreBaked Grafana Template

```json
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": {
          "type": "grafana",
          "uid": "-- Grafana --"
        },
        "enable": true,
        "hide": true,
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "id": null,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "collapsed": false,
      "gridPos": {
        "h": 4,
        "w": 6,
        "x": 0,
        "y": 0
      },
      "id": 1,
      "title": "Total Runs",
      "type": "stat",
      "datasource": {
        "type": "yesoreyeram-infinity-datasource",
        "uid": "infinity"
      },
      "targets": [
        {
          "datasource": {
            "type": "yesoreyeram-infinity-datasource",
            "uid": "infinity"
          },
          "type": "json",
          "source": "url",
          "url": "http://localhost:3004/api/v1/workspaces/${workspaceId}/projects/${projectId}/metrics",
          "root_selector": "",
          "columns": [],
          "filters": [],
          "format": "table",
          "refId": "A"
        }
      ],
      "fieldConfig": {
        "defaults": {
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          }
        },
        "overrides": []
      },
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "percentChangeColorMode": "value",
        "reduceOptions": {
          "calcs": [
            "count"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      }
    },
    {
      "collapsed": false,
      "gridPos": {
        "h": 4,
        "w": 6,
        "x": 6,
        "y": 0
      },
      "id": 2,
      "title": "Passed Tests Rate",
      "type": "gauge",
      "datasource": {
        "type": "yesoreyeram-infinity-datasource",
        "uid": "infinity"
      },
      "targets": [
        {
          "datasource": {
            "type": "yesoreyeram-infinity-datasource",
            "uid": "infinity"
          },
          "type": "json",
          "source": "url",
          "url": "http://localhost:3004/api/v1/workspaces/${workspaceId}/projects/${projectId}/metrics",
          "refId": "A"
        }
      ],
      "fieldConfig": {
        "defaults": {
          "unit": "percent",
          "min": 0,
          "max": 100,
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "red",
                "value": null
              },
              {
                "color": "yellow",
                "value": 70
              },
              {
                "color": "green",
                "value": 90
              }
            ]
          }
        },
        "overrides": []
      }
    },
    {
      "collapsed": false,
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 0,
        "y": 4
      },
      "id": 3,
      "title": "Recent Test Runs Duration",
      "type": "timeseries",
      "datasource": {
        "type": "yesoreyeram-infinity-datasource",
        "uid": "infinity"
      },
      "targets": [
        {
          "datasource": {
            "type": "yesoreyeram-infinity-datasource",
            "uid": "infinity"
          },
          "type": "json",
          "source": "url",
          "url": "http://localhost:3004/api/v1/workspaces/${workspaceId}/projects/${projectId}/metrics",
          "refId": "A"
        }
      ],
      "options": {
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom",
          "showLegend": true
        },
        "tooltip": {
          "mode": "single",
          "sort": "none"
        }
      }
    }
  ],
  "schemaVersion": 38,
  "style": "dark",
  "tags": [
    "rova",
    "qa",
    "observability"
  ],
  "title": "Rova Test Suite Metrics",
  "version": 1
}

```
