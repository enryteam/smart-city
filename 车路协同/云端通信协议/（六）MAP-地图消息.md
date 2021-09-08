[TOC]

【定义】
地图消息。<font color='red'>由路侧单元广播，向车辆传递局部区域的地图信息。包括局部区域的路口信息、路段信息、车道信息，道路之间的连接关系等。</font>

单个地图消息可以包含多个路口或区域的地图数据。路口处的信号灯信息则在SPAT消息中详细定义。

图42给出了MAP消息的主体结构，是一个层层嵌套的形式。其中实线框为必有项，虚线框为可选项。

![image-20210609095438097](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210609095438097.png)



# 一、MAP地图消息	广播给OBU 持续发送  100毫秒

```json
{
    "_id" : "5f9f9c15a072630079e419a9",
    "msgCnt" : 40,
    "timeStamp" : null,
    "nodes" : [  // 本RSU接收到的经纬度点信息发送出去    //代表一个地图： 标注点的经纬度  数组
        {
            "name" : null,//烟台大学里路名
            "id" : { //
                "region" : 1,
                "id" : 10
            },
            "refPos" : { // 选一个基准点
                "lat" : 281128561,
                "long_" : 1128668111,
                "elevation" : null
            },
            "inLinks" : [ 
                {
                    "name" : null, //
                    "upstreamNodeId" : {  //上游是原理
                        "region" : 1,
                        "id" : 101
                    },
                    "speedLimits" : null, 速度显示
                    "laneWidth" : 350, 车道宽度
                    "points" : null,   // 
                    "movements" : null,// 绑定相位ID   ：直行，左转
                    "lanes" : [ 
                        {
                            "laneID" : 11,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null  //和maneuvers实现方式不同，意义差不多
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 7860,
                                                "lat" : 14590
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 360,
                                                "lat" : 2220
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 12,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 2
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 8210,
                                                "lat" : 14470
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 640,
                                                "lat" : 2130
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 13,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 1
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 8590,
                                                "lat" : 14330
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 920,
                                                "lat" : 1990
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 102
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 21,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 11
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1900,
                                                "lat" : 1560
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 4080,
                                                "lat" : 5130
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 22,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 11
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1600,
                                                "lat" : 1700
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 3760,
                                                "lat" : 5250
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 23,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 11
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1340,
                                                "lat" : 1800
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 3450,
                                                "lat" : 5370
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 103
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 31,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 14280,
                                                "lat" : -5170
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 2210,
                                                "lat" : 260
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 32,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 6
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 14090,
                                                "lat" : -5440
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 2030,
                                                "lat" : -40
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 33,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 5
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : 13930,
                                                "lat" : -5700
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1810,
                                                "lat" : -330
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 104
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 41,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 12
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1150,
                                                "lat" : -1400
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 5070,
                                                "lat" : -3000
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 42,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 12
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1300,
                                                "lat" : -1150
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 5210,
                                                "lat" : -2770
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 43,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 12
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : 1520,
                                                "lat" : -910
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : 5360,
                                                "lat" : -2500
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 105
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 51,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -7790,
                                                "lat" : -14280
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -80,
                                                "lat" : -1880
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 52,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 10
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -8090,
                                                "lat" : -14140
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -460,
                                                "lat" : -1750
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 53,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 9
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -8430,
                                                "lat" : -14020
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -800,
                                                "lat" : -1610
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 106
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 61,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 13
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1810,
                                                "lat" : -1180
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -2970,
                                                "lat" : -3120
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 62,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 13
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1450,
                                                "lat" : -1320
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -2630,
                                                "lat" : -3250
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 63,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 13
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1120,
                                                "lat" : -1500
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -2280,
                                                "lat" : -3370
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 107
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 71,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -12990,
                                                "lat" : 5170
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -2070,
                                                "lat" : -100
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 72,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 14
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -12790,
                                                "lat" : 5380
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1870,
                                                "lat" : 200
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 73,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 10
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : 13
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 2,
                                            "position_LL1" : null,
                                            "position_LL2" : null,
                                            "position_LL3" : {
                                                "lon" : -12570,
                                                "lat" : 5650
                                            },
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1720,
                                                "lat" : 440
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }, 
                {
                    "name" : null,
                    "upstreamNodeId" : {
                        "region" : 1,
                        "id" : 108
                    },
                    "speedLimits" : null,
                    "laneWidth" : 350,
                    "points" : null,
                    "movements" : null,
                    "lanes" : [ 
                        {
                            "laneID" : 81,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 14
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1140,
                                                "lat" : 1560
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -3850,
                                                "lat" : 2700
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 82,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 14
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1280,
                                                "lat" : 1340
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -4040,
                                                "lat" : 2420
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }, 
                        {
                            "laneID" : 83,
                            "laneAttributes" : null,
                            "maneuvers" : null,
                            "connectsTo" : [ 
                                {
                                    "remoteIntersection" : {
                                        "region" : 1,
                                        "id" : 14
                                    },
                                    "connectingLane" : null,
                                    "phaseId" : null
                                }
                            ],
                            "speedLimits" : null,
                            "points" : [ 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 0,
                                            "position_LL1" : {
                                                "lon" : -1440,
                                                "lat" : 1060
                                            },
                                            "position_LL2" : null,
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }, 
                                {
                                    "posOffset" : {
                                        "offsetLL" : {
                                            "choiceID" : 1,
                                            "position_LL1" : null,
                                            "position_LL2" : {
                                                "lon" : -4140,
                                                "lat" : 2130
                                            },
                                            "position_LL3" : null,
                                            "position_LL4" : null,
                                            "position_LL5" : null,
                                            "position_LL6" : null,
                                            "position_LatLon" : null
                                        },
                                        "offsetV" : null
                                    }
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```





# 二、字段说明

## 2.1 timeStamp	MinuteOfTheYear OPTIONAL时间戳

```ASN.1
【定义】
数值用来表示当前年份，已经过去的总分钟数（UTC 时间）。分辨率为1 分钟。该数值配合
DSecond 数值，则可表示全年已过去的总毫秒数。
【ASN.1 代码】
MinuteOfTheYear ::= INTEGER (0..527040)
-- the value 527040 shall be used for invalid
```

## 2.2 msgCnt	MsgCount 消息计数

```ASN.1
【定义】 
发送方为自己发送的同类消息，依次进行编号。编号数值为 0 ～ 127。 
当发送方开始发起某一类数据时，它可以随机选择起始编号，随后依次递增。发送方也可以在连续发送相同的数据帧时，选择使用相同的 MsgCount 消息编号。编号到达 127 后，则下一个回到 0。 
【ASN.1 代码】 
MsgCount ::= INTEGER (0..127)
```

## 2.3 nodes地图节点（NodeList）

- nodes：地图节点，地图的基本组成部分。
- 可以是交叉路口，也可以使一个路段的断点。
- 在地图上，相邻且有序的两个节点确定一条有向路段。
- 十字路口或者道路终点



节点属性包括：

- 名称
- ID
- 位置
- 节点相连的上游路段集合

【定义】 
地图节点。节点是地图的最基本组成部分，可以是交叉路口，也可以是一个路段的端点。
在地图上，相邻且有序的两个节点确定一条有向路段。 
节点属性包括名称、ID、位置以及与<font color='red'>节点相连的上游路段集合。 </font>
<font color='red'>节点数据帧中包含的路段列表，均以该节点作为下游端点。而以该节点为上游端点的路段，则归属于该路段下游节点的数据帧。 </font>

```ASN.1
【ASN.1 代码】 
Node ::= SEQUENCE { 
-- Node can be an intersection, or a road endpoint 
name DescriptiveName OPTIONAL, 
-- Node name 
id NodeReferenceID, 
-- A globally unique value set, 
-- consisting of a regionID and 
-- node ID assignment 
refPos Position3D, 
-- 3D position of the center of this Node. 
-- This position is also the reference position for the elements inside 
inLinks LinkList OPTIONAL, 
-- all the links enter this Node 
... 
}
```

### Seq.of Node sequence of node	节点序列



#### 1. name DescriptiveName名称

```ASN.1
【定义】 
定义名称字符串类型。 
【ASN.1 代码】 
DescriptiveName ::= IA5String (SIZE(1..63))
```

#### 2. id NodeID节点编号

```ASN.1
【定义】 
定义节点 ID。路网最基本的构成即节点和连接节点的路段。节点可以是路口，也可以是一条 
路的端点。一个节点的 ID 在同一个区域内是唯一的。数值 0 ～ 255 预留为测试使用。 
【ASN.1 代码】 
NodeID ::= INTEGER (0..65535) 
-- The values zero through 255 are allocated for testing purposes 
-- Note that the value assigned to a node will be 
-- unique within a given regional ID only
```

#### 3. refPos（3D） reference position（Position3D）参考位置

```ASN.1
【定义】
三维的坐标位置，包括经纬度和高程。
【ASN.1 代码】
Position3D := SEQUENCE{
lat Latitude,
--in I/10th micro degrees
 long Longitude, 
--in I/10th micro degrees
elevation Elevation OPTIONAL 
-- in 10 cm units
}
```

- lat Latitude纬度

```ASN.1
【定义】
定义纬度数值，北纬为正，南纬为负。分辨率1e-7°。
【ASN.1 代码】
Latitude:= INTEGER(-900000.9000001)
--LSB= 1/10 micro degree
--Providing a range of plus-minus 90 degrees
```

- long Longitude经度

```ASN.1
【定义】
定义经度数值。东经为正，西经为负。分辨率为1e-7°。
【ASN.1 代码】
Longitude ::= INTEGER(-17999999..180000001)
-- ISB= 1/10 micro degree 
-- Providing a range of plus-minus 180 degrees
```

- elevation Elevation OPTIONAL 海拔

```ASN.1
【定义】
定义车辆海拔高程。分辨率为0.1米。数值-4096 表示无效数值。【ASN.1 代码】
Elevation ::= INTEGER (-4096..61439)
-- In units of 10cm steps above or below the reference ellipsoid
-- Providing a range of-409.5 to＋6143.9 meters
-- The value-4096 shall be used when Unknown is to be sent
```

### inLinks LinkList链表 

Seq.of Link sequence of Link	链接序列

#### 1. name DescriptiveName名称

```ASN.1
【定义】 
定义名称字符串类型。 
【ASN.1 代码】 
DescriptiveName ::= IA5String (SIZE(1..63))
```

#### 2. upstreamNodeId上行节点编号

```ASN.1
【定义】 
定义路段或车道的限速列表。 
【ASN.1 代码】 
SpeedLimitList ::= SEQUENCE (SIZE(1..9)) OF RegulatorySpeedLimit
```

- RegulatorySpeedLimit限速属性

```ASN.1
【定义】
定义限速属性。包括限速类型以及所规定的限速值。
【ASN.1 代码】
RegulatorySpeedLimit ::=SEQUENCE {
type SpeedLimitType,
-- The type of regulatory speed which folows 

speed Speed
-- The speed in units of 0.02 m/s
-- See Section 11 for converting and translating
-- speed expressed in mph into units of m/s
}
```

- -  type SpeedLimitType限速类型

  ```ASN.1
  【定义】
  定义限速类型，指示给出的限速大小对应的参考类型。
  【ASN.1代码】
  SpeedLimitType ::= ENUMERATED{
  unknown,-- Speed limit type not available 
  maxSpeedInSchoolZone,--Only sent when the limit is active 
  maxSpeedInSchoolZone WhenChildrenArePresent,-- Sent at any time 
  maxSpeedlnConstuctionZone,-- Used forwork zones, incident zones,etc.
  -- where a reduced speed is present 
  vehicleMinSpeed,
  vehicleMaxSpeed,--Regulatory speed limit for general traffic 
  vehicleNightMaxSpeed, 
  truckMinSpeed, 
  truckMaxSpeed,
  truckNightMaxSpeed, 
  vehiclesWithTrailersMinSpeed, 
  vehicles WithTrailersMaxSpeed, 
  vehiclesWithTrailersNight MaxSpeed,
  ...
  }
  ```

  - speed Speed车速

  - ```ASN.1
    【定义】
    车速大小。分辨率为0.02m/s。数值8191表示无效数值。
    【ASN.1 代码】
    Speed ::=INTEGER(0.8191)
    -- Units of 0.02 m/s
    --The value 8191 indicates that
    -- speed is unavailable
    ```

  

#### 3. laneWidth车道宽度

```ASN.1
【定义】
定义车道宽度。分辨率为1cm。
【ASN.1 代码】
LaneWidth= INTEGER(0..32767)
-- units of 1 cm
```

#### Seq.of Lane sequence of lane 车道系列

##### 1. laneID车道编号

```ASN.1
【定义】
定义车道ID。每一条有向路段上的每个车道，都拥有一个单独的ID。数值0表示无效ID。
【ASN.1 代码】
LaneID ::= INTEGER (0..255) 
-- the value 0 shall be used when the lane ID is
-- not available or not known
-- the value 255 is reserved for future use
```

##### 2. laneAttributes车道属性

```ASN.1
【定义】
定义车道属性。包括车道共享情况以及车道本身所属的类别特性。
【ASN.1代码】
LaneAttributes ::= SEQUENCE {
shareWith LaneSharing OPTIONAL, 
laneType LaneTypeAttributes
}
```

- sharewith LaneSharing车道被共享情况

```ASN.1
【定义】
定义车道被共享的情况。在已有的车道属性定义基础上，该数据表示此车道还会有其他的交通参与者者出现，并可能拥有相同的路权。数据每一个比特位，如果是"1"，则表示对应的车道共享属性生效。
【ASN.1 代码】
LaneSharing ::= BIT STRING{
--With bits as defined:
overlappingLaneDescriptionProvided (0),
-- Assert when another lane object is present to describe the
-- path of the overlapping shared lane
--this construct is not used for lane objects which simply cross 

multipleLanesTreatedAsOneLane (1),
--Assert if the lane object path and width details represents
-- multiple lanes within it that are not further described
-- Various modes and type of raffic that may share this lane: 

otherNonMotorizedTafficTypes (2),--horse drawn etc. 
individualMotorizedVehicleTraffic (3),
busVehicleTraffic (4), 
taxiVehicleTraffic (5), 
pedestriansTraffic (6), 
cyclistVehicleTraffic (7),
trackedVehicleTraffic (8), 
pedestrianTraffic (9)
} (SIZE (10))
-- Allzeros would indicate'not shared'and'not overlapping'
```

- laneType LaneTypeAttributes车道属性

```ASN.1
【定义】
定义不同类别车道的属性集合。
【ASN.1 代码】
LaneTypeAttributes ::= CHOICE {
vehicle LaneAttributes-Vehicle,-- motor vehicle lanes 
crosswalk LaneAttributes-Crosswalk,-- pedestrian crosswalks 
bikeLane LaneAttributes-Bike,-- bike lanes
sidewalk LaneAttributes-Sidewalk,-- pedestrian sidewalk paths
median LaneAttributes-Barrier,-- medians& channelization 
striping LaneAttributes-Striping,-- roadway markings 
trackedVehicle LaneAttributes-TrackedVehicle,-- trains and trolleys 
parking LaneAttributes-Parking,-- parking and stopping lanes
...
}
```

##### 3. maneuvers AllowedManeuvers允许转向行为

```ASN.1
【定义】 
定义一个（机动车）车道的允许转向行为。 
【ASN.1 代码】 
AllowedManeuvers ::= BIT STRING { 
-- With bits as defined: 
-- Allowed maneuvers at path end (stop line) 
-- All maneuvers with bits not set are therefore prohibited 
-- A value of zero shall be used for unknown, indicating no Maneuver 
maneuverStraightAllowed (0), 
-- a Straight movement is allowed in this lane
maneuverLeftAllowed (1), 
-- a Left Turn movement is allowed in this lane 
maneuverRightAllowed (2), 
-- a Right Turn movement is allowed in this lane 
maneuverUTurnAllowed (3), 
-- a U turn movement is allowed in this lane 
maneuverLeftTurnOnRedAllowed (4), 
-- a Stop, and then proceed when safe movement 
-- is allowed in this lane 
maneuverRightTurnOnRedAllowed (5), 
-- a Stop, and then proceed when safe movement 
-- is allowed in this lane 
maneuverLaneChangeAllowed (6), 
-- a movement which changes to an outer lane 
-- on the egress side is allowed in this lane 
-- (example: left into either outbound lane) 
maneuverNoStoppingAllowed (7), 
-- the vehicle should not stop at the stop line 
-- (example: a flashing green arrow) 
yieldAllwaysRequired (8), 
-- the allowed movements above are not protected 
-- (example: an permanent yellow condition) 
goWithHalt (9), 
-- after making a full stop, may proceed 
caution (10), 
-- proceed past stop line with caution 
reserved1 (11) 
-- used to align to 12 Bit Field 
} (SIZE(12))
```

##### 4. connectsTo ConnectsToList连接关系列表

```ASN.1
【定义】 
定义路段中每条车道在下游路口处与下游路段车道的转向连接关系列表。 
【ASN.1 代码】 
ConnectsToList ::= SEQUENCE (SIZE(1..8)) OF Connection
```

Seq.of Connection sequence of connection 车道与下游路段车道的连接关系序列

```ASN.1
【定义）
定义车道与下游路段车道的连接关系。包括下游路段出口节点ID、连接的下游路段车道基本信息以及对应的信号灯相位号。在车道连接中定义的相位号，是对 DF_Movement中定义转向的相位号的一个补充。当某一些车道在转向时需要参考一些特殊的信号灯相位（而不是 DF_Movement中定义的默认相位），则应该将其定义在本数据帧中。
【ASN.1 代码】 
Connecton:=SEQUENCE{
 remotelntersection NodeReferenceID,
--This entry indicates the downstream intersection of the link this lane connects to.
-- This provides a means to create meshes of lanes

connectingLane ConnectingLane OPTIONAL,
--The index of the connecting lane and also
--the maneuver from the current lane to it
-- When we want to list the allwed lanes of the next link
-- this lane can lead to,we use this entry 

phaseld PhaseID OPTIONAL
--The matching signal group send by
-- the SPAT message for this lane/maneuver.
--Shall be present unless the connectingLane 
--has no signal group is un-signalized)
}
```

- remotelntersection NodeReferenceID参考ID

- ```ASN.1
  【定义】
  定义参考ID。参考ID由一个全局唯一的地区ID和一个地区内部唯一的节点D组成。
  【ASN.1 代码】
  NodeReferenceID ::= SEQUENCE {
  region RoadRegulatorID OPTIONAL,
  -- a globally unique regional assignment value
  -- typical assigned to a regional DOT authority
  -- the value zero shall be used for testing needs 
  
  id NodeID,
  -- a unique mapping to the node
  -- in question within the above region of use
  
  }
  ```

- - region RoadRegulatorID OPTIONAL地图中各个划分区域的ID号

  - ```ASN.1
    【定义】
    定义地图中各个划分区域的ID号。数值0仅用于测试。
    【ASN.1 代码】
    RoadRegulatorID ::= INTEGER (0..65535)
    --The value zero shall be used for testing only
    ```

  - id NodeID节点ID

  - ```ASN.1
    【定义】
    定义节点ID。路网最基本的构成即节点和连接节点的路段。节点可以是路口，也可以是一条路的端点。一个节点的ID在同一个区域内是唯一的。数值0～255 预留为测试使用。
    【ASN.1 代码】
    NodeID ::= INTEGER (0..65535)
    -- The values zero through 255 ar allocated for testing purposes
    -- Note that the value assigned to a node will be
    -- unique within a given regional ID only
    ```

- connectingLane ConnectingLane OPTIONAL连接车道

- ```ASN.1
  【定义】
  用于定位上游车道转向连接的下游车道，包括车道ID以及该转向的允许行驶行为。这里，下游车道 ID 的作用范围是其所在的路段。
  【ASN.1 代码】
  ConnectingLane ::=SEQUENCE {
  lane LanelD,
  -- Index of the connecting lane 
  
  maneuver AllowedManeuvers OPTIONAL
  -- The Maneuver between 
  -- the enclosing lane and this lane 
  --at the stop line to connect them
  
  }
  ```

- - lane LaneID车道ID

  - ```ASN.1
    【定义】
    定义车道ID。每一条有向路段上的每个车道，都拥有一个单独的ID。数值0表示无效ID。
    【ASN.1 代码】
    LaneID ::= INTEGER (0..255)
    -- the value 0 shall be used when the lane ID is
    -- not available or not known
    -- the value 255 is reserved for future use
    ```

  - maneuver AllowedManeuvers OPTIONAL车道的允许转向行为

  - ```ASN.1
    【定义】
    定义一个（机动车）车道的允许转向行为。
    【ASN.1 代码】
    AllowedManeuvers ::= BIT STRING {
    --With bits as defined:
    --Allowed maneuvers at path end (stop line)
    --All maneuvers with bits not set are therefore prohibited
    --A value of zero shall be used for unknown,indicating no Maneuver 
    maneuverStraightAllowed (0),
    --a Straight movement is allowed in this lane
    maneuverLeftAllowed (1),
    --a Left Turn movement is allowed in this lane 
    maneuverRightAllowed (2),
    --a Right Turn movement is allowed in this lane
    maneuverUTurnAllowed (3),
    --a U turn movement is allowed in this lane 
    maneuverLeftTurnOnRedAllowed (4),
    --a Stop, and then proceed when safe movement
    --is allowed in this lane
    maneuverRightTurnOnRedAllowed (5),
    --a Stop, and then proceed when safe movement
    --is allowed in this lane
    maneuverLaneChangeAllowed (6),
    --a movement which changes to an outer lane
    -- on the egress side is allowed in this lane
    --(example: left into either outbound lane) 
    maneuverNoStoppingAllowed (7),
    --the vehicle should not stop at the stop line
    --(example: a flashing green arrow) 
    yieldAllwaysRequired (8),
    --the allowed movements above are not protected
    --(example: an permanent yellow condition) 
    goWithHalt (9),
    --after making a full stop, may proceed 
    caution (10),
    --proceed past stop line with caution 
    reserved1 (11)
    --used to align to12 Bit Field
    } (SIZE(12))
    ```

- phaseId相位 ID

- ```ASN.1
  【定义】
  定义信号灯相位 ID。数值o表示无效ID。
  【ASN.1 代码】
  PhaseID ::= INTEGER (0..255)
  --The value 0 shall be used when the ID is not available or not known
  ```



##### 5. points PointList点

```ASN.1
【定义】 
定义一个有向路段上的中间位置点列表，用来表达路段上截面或片段的特殊属性。列表中所有 
位置点需按上游至下游顺序排列。 
【ASN.1 代码】 
PointList ::= SEQUENCE (SIZE(2..31)) OF RoadPoint
-- At least 2 points of 1 lane 
-- entry line and exit line 
-- points need to be listed sequatially 
-- from upstream to downstream
```



Seq.of RoadPoint sequence of roadpoint整道路上标记的一个位置点属性序列

```ASN.1
【定义】
表示完整道路上标记的一个位置点属性。包括相对位置、位置点处路段截面的特殊属性集合，以及该位置点到下游相邻位置点之间局部路段的特殊属性集合。如果位置点为路段最下游的点，则其包含的下游截取路段属性为无效数据。
【ASN.1 代码】 
RoadlPoint::=SEQUENCE {
posOffset PositionOffsetLLV,
-- Position offset to the reference position
..
}
```

##### 6. speedLimits SpeedLimitList 速度限制

```ASN.1
【定义】 
定义路段或车道的限速列表。 
【ASN.1 代码】 
SpeedLimitList ::= SEQUENCE (SIZE(1..9)) OF RegulatorySpeedLimit
```

RegulatorySpeedLimit限速属性

```ASN.1
【定义】
定义限速属性。包括限速类型以及所规定的限速值。
【ASN.1 代码】
RegulatorySpeedLimit ::=SEQUENCE {
type SpeedLimitType,
-- The type of regulatory speed which folows 
speed Speed
-- The speed in units of 0.02 m/s
-- See Section 11for converting and translating
-- speedexpressed in mph into units of m/s
}
```

- type SpeedLimitType限速类型

- ```ASN.1
  【定义】
  定义限速类型，指示给出的限速大小对应的参考类型。
  【ASN.1代码】
  SpeedLimitType ::= ENUMERATED{
  unknown,-- Speed limit type not available
  maxSpeedInSchoolZone,--Only sent when the limit is active
  maxSpeedInSchoolZoneWhenChildrenArePresent,-- Sent at any time 
  maxSpeedlnConstuctionZone,-- Used for work zones, incident zones,etc.
  -- where a reduced speed is present 
  vehicleMinSpeed,
  vehicleMaxSpeed,--Regulatory speed limit for general traffic 
  vehicleNightMaxSpeed, 
  truckMinSpeed, 
  truckMaxSpeed, 
  truckNightMaxSpeed, 
  vehiclesWithTrailersMinSpeed, 
  vehicle WithTrailersMaxSpeed, 
  vehiclesWithTrailerNightMaxSpeed,
  ...
  }
  ```

- speed Speed车速

- ```ASN.1
  【定义】
  车速大小。分辨率为0.02m/s。数值8191表示无效数值。
  【ASN.1 代码】
  Speed ::=INTEGER(0..8191)
  -- Units of 0.02 m/s
  --The value 8191 indicates that
  -- speed is unavailable
  ```



### points PointList点

```ASN.1
【定义】 
定义一个有向路段上的中间位置点列表，用来表达路段上截面或片段的特殊属性。列表中所有 
位置点需按上游至下游顺序排列。 
【ASN.1 代码】 
PointList ::= SEQUENCE (SIZE(2..31)) OF RoadPoint
-- At least 2 points of 1 lane 
-- entry line and exit line 
-- points need to be listed sequatially 
-- from upstream to downstream
```

seq of RoadPoint完整道路上标记的一个位置点属性

```ASN.1
【定义】
表示完整道路上标记的一个位置点属性。包括相对位置、位置点处路段截面的特殊属性集合，以及该位置点到下游相邻位置点之间局部路段的特殊属性集合。如果位置点为路段最下游的点，则其包含的下游截取路段属性为无效数据。
【ASN.1 代码】
RoadPoint ::= SEQUENCE{
posOffset PositionOffsetLLV,
-- Position offset to the reference position
...
}
```



### Movements移动

```ASN.1
【定义】
描述道路与下游路段的连接关系，以及该连接对应的本地路口处信号灯相位ID。此处的相位 ID事实上也是MAP消息与SPAT消息的唯一关联。车辆在确定转向行为后，能够通过该相位ID数据，查看到SPAT中对应的相位实时状态，从而获得行车过程中的信号灯数据辅助。 
【ASN.1 代码】
Movement ::= SEQUENCE {
remotelntersection NodeReferenceID,
--This entry indicates the downstream intersection of the link this lane connects to. 
--This provides a means to create meshes of lanes 

phaseld PhaseID OPTIONAL 
--The matching signal group send by 
--the SPAT message for this lane/maneuver. 
--Shall be present unless the connectingLane 
-- has no signal group (is un-signalized)
}
```

Seq.of Movements sequence of movements移动序列

- remotelntersection NodeReferenceID参考ID

- ```ASN.1
  【定义】
  定义参考ID。参考ID由一个全局唯一的地区ID和一个地区内部唯一的节点D组成。
  【ASN.1 代码】
  NodeReferenceID ::= SEQUENCE {
  region RoadRegulatorID OPTIONAL,
  -- a globally unique regional assignment value
  -- typical assigned to a regional DOT authority
  -- the value zero shall be used for testing needs 
  
  id NodeID,
  -- a unique mapping to the node
  -- in question within the above region of use
  }
  ```

- - region RoadRegulatorID OPTIONAL地图中各个划分区域的ID号

  - ```ASN.1
    【定义】
    定义地图中各个划分区域的ID号。数值0仅用于测试。
    【ASN.1 代码】
    RoadRegulatorID ::= INTEGER (0..65535)
    --The value zero shall be used for testing only
    ```

  - id NodeID节点ID

  - ```ASN.1
    【定义】
    定义节点ID。路网最基本的构成即节点和连接节点的路段。节点可以是路口，也可以是一条路的端点。一个节点的ID在同一个区域内是唯一的。数值0～255 预留为测试使用。
    【ASN.1 代码】
    NodeID ::= INTEGER (0..65535)
    -- The values zero through 255 ar allocated for testing purposes
    -- Note that the value assigned to a node will be
    -- unique within a given regional ID only
    ```

- phaseId相位 ID

- ```ASN.1
  【定义】
  定义信号灯相位 ID。数值o表示无效ID。
  【ASN.1 代码】
  PhaseID ::= INTEGER (0..255)
  --The value 0 shall be used when the ID is not available or not known
  ```



### lanes LaneList

```ASN.1
【定义】
定义一个路段中包含的车道列表。
【ASN.1 代码】
LaneList ::= SEQUENCE(SIZE1..32)OFLane
```

Seq.of Lane sequence of lane道路序列

```ASN.1
【定义】 
定义车道。包含其 ID、共享属性、车道出口的允许转向行为、车道与下游路段车道的连接关 
系列表，以及车道中间点列表。 
【ASN.1 代码】 
Lane ::= SEQUENCE { 
laneID LaneID, 
-- The unique ID number assigned 
-- to this lane object 
laneAttributes LaneAttributes OPTIONAL, 
-- Define basic attribute of lane 
maneuvers AllowedManeuvers OPTIONAL, 
-- the permitted maneuvers for this lane 
connectsTo ConnectsToList OPTIONAL, 
-- connection to downsteam lanes 
speedLimits SpeedLimitList OPTIONAL,
--List all the speed limits 
points PointList OPTIONAL,
-- Define road points and segments
..
}
```

- laneID车道编号

```ASN.1
【定义】
定义车道ID。每一条有向路段上的每个车道，都拥有一个单独的ID。数值0表示无效ID。
【ASN.1 代码】
LaneID ::= INTEGER (0..255)
-- the value 0 shall be used when the lane ID is
-- not available or not known
-- the value 255 is reserved for future use
```

- laneAttributes车道属性

```ASN.1
【定义】
定义车道属性。包括车道共享情况以及车道本身所属的类别特性。
【ASN.1代码】
LaneAttributes ::= SEQUENCE {
shareWith LaneSharing OPTIONAL, 
laneType LaneTypeAttributes
}
```

- - sharewith LaneSharing车道被共享情况

  - ```ASN.1
    【定义】
    定义车道被共享的情况。在已有的车道属性定义基础上，该数据表示此车道还会有其他的交通参与者者出现，并可能拥有相同的路权。数据每一个比特位，如果是"1"，则表示对应的车道共享属性生效。
    【ASN.1 代码】
    LaneSharing ::= BIT STRING{
    --With bits as defined:
    
    overlappingLaneDescriptionProvided (0),
    -- Assert when another lane object is present to describe the
    -- path of the overlapping shared lane
    --this construct is not used for lane objects which simply cross 
    
    multipleLanesTreatedAsOneLane (1),
    --Assert if the lane object path and width details represents
    --multiple lanes  within it that are not further described
    --Various modes and type of traffic that may share this lane:
    
    otherNonMotorizedTafficTypes (2),--horse drawn etc. 
    individualMotorizedVehicleTraffic (3),
    busVehicleTraffic (4), 
    taxiVehicleTraffic (5), 
    pedestriansTraffic (6), 
    cyclistVehicleTraffic (7),
    trackedVehicleTraffic (8), 
    pedestrianTraffic (9)
    } (SIZE (10))
    -- Allzeros would indicate'not shared'and'not overlapping
    ```

  - laneType LaneTypeAttributes车道属性

  - ```ASN.1
    【定义】
    定义不同类别车道的属性集合。
    【ASN.1 代码】
    LaneTypeAttributes ::= CHOICE {
    vehicle LaneAttributes-Vehicle,-- motor vehicle lanes 
    crosswalk LaneAttributes-Crosswalk,-- pedestrian crosswalks 
    bikeLane LaneAttributes-Bike,-- bike lanes
    sidewalk LaneAttributes-Sidewalk,-- pedestrian sidewalk paths 
    median LaneAttributes-Barrier,-- medians& channelization 
    striping LaneAttributes-Striping,-- roadway markings
    trackedVehicle LaneAttributes-TrackedVehicle,-- trains and trolleys 
    parking LaneAttributes-Parking,-- parking and stopping lanes
    ...
    }
    ```

- maneuvers AllowedManeuvers允许转向行为

- ```ASN.1
  【定义】 
  定义一个（机动车）车道的允许转向行为。 
  【ASN.1 代码】 
  AllowedManeuvers ::= BIT STRING { 
  -- With bits as defined: 
  -- Allowed maneuvers at path end (stop line) 
  -- All maneuvers with bits not set are therefore prohibited 
  -- A value of zero shall be used for unknown, indicating no Maneuver 
  maneuverStraightAllowed (0), 
  -- a Straight movement is allowed in this lane 
  maneuverLeftAllowed (1), 
  -- a Left Turn movement is allowed in this lane 
  maneuverRightAllowed (2), 
  -- a Right Turn movement is allowed in this lane 
  maneuverUTurnAllowed (3), 
  -- a U turn movement is allowed in this lane 
  maneuverLeftTurnOnRedAllowed (4), 
  -- a Stop, and then proceed when safe movement 
  -- is allowed in this lane 
  maneuverRightTurnOnRedAllowed (5), 
  -- a Stop, and then proceed when safe movement 
  -- is allowed in this lane 
  maneuverLaneChangeAllowed (6), 
  -- a movement which changes to an outer lane 
  -- on the egress side is allowed in this lane 
  -- (example: left into either outbound lane) 
  maneuverNoStoppingAllowed (7), 
  -- the vehicle should not stop at the stop line 
  -- (example: a flashing green arrow) 
  yieldAllwaysRequired (8), 
  -- the allowed movements above are not protected 
  -- (example: an permanent yellow condition) 
  goWithHalt (9), 
  -- after making a full stop, may proceed 
  caution (10), 
  -- proceed past stop line with caution 
  reserved1 (11) 
  -- used to align to 12 Bit Field 
  } (SIZE(12))
  ```

- connectsTo ConnectsToList连接关系列表

- ```ASN.1
  【定义】 
  定义路段中每条车道在下游路口处与下游路段车道的转向连接关系列表。 
  【ASN.1 代码】 
  ConnectsToList ::= SEQUENCE (SIZE(1..8)) OF Connection
  ```

- - Seq.of Connection sequence of connection 车道与下游路段车道的连接关系序列

  - ```ASN.1
    【定义）
    定义车道与下游路段车道的连接关系。包括下游路段出口节点ID、连接的下游路段车道基本信息以及对应的信号灯相位号。在车道连接中定义的相位号，是对 DF_Movement中定义转向的相位号的一个补充。当某一些车道在转向时需要参考一些特殊的信号灯相位（而不是 DF_Movement中定义的默认相位），则应该将其定义在本数据帧中。
    【ASN.1 代码】 
    Connection::=SEQUENCE{
    remotelntersection NodeReferenceID, 
    --This entry indicates the downstream intersection of the link this lane connects to.
    -- This provides a means to create meshes of lanes 
    
    connectingLane ConectingLane OPTIONAL,
    --The index of the connecting lane and also
    --the maneuver from the current lane to it
    -- When we want to list the allwed lanes of the next link
    -- this lane can lead to,we use this entry 
    
    phaseld PhaseID OPTIONAL
    --The matching signal group send by
    -- the SPAT message for this lane/maneuver.
    --Shall be present unless the connectingLane 
    --has no signal group (is un-signalized)
    
    }
    ```

  remotelntersection NodeReferenceID参考ID

  ```ASN.1
  【定义】
  定义参考ID。参考ID由一个全局唯一的地区ID和一个地区内部唯一的节点D组成。
  【ASN.1 代码】
  NodeReferencID ::= SEQUENCE {
  region RoadRegulatorID OPTIONAL,
  -- a globally unique regional assignment value
  -- typical assigned to a regional DOT authority
  -- the value zero shall be used for testing needs 
  
  id NodeID,
  -- a unique mapping to the node
  -- in question within the above region of use
  
  }
  ```

  region RoadRegulatorID OPTIONAL地图中各个划分区域的ID号

  ```ASN.1
  【定义】
  定义地图中各个划分区域的ID号。数值0仅用于测试。
  【ASN.1 代码】
  RoadRegulatorID ::= INTEGER (0..65535)
  --The value zero shall be used for testing only
  ```

  id NodeID节点ID

  ```ASN.1
  【定义】
  定义节点ID。路网最基本的构成即节点和连接节点的路段。节点可以是路口，也可以是一条路的端点。一个节点的ID在同一个区域内是唯一的。数值0～255 预留为测试使用。
  【ASN.1 代码】
  NodeID ::= INTEGER (0..65535)
  -- The values zero through 255 are allocated for testing purposes
  -- Note that the value assigned to a node will be
  -- unique within a given regional ID only
  ```

  connectingLane ConnectingLane OPTIONAL连接车道

  ```ASN.1
  【定义】
  用于定位上游车道转向连接的下游车道，包括车道ID以及该转向的允许行驶行为。这里，下游车道 ID 的作用范围是其所在的路段。
  【ASN.1 代码】
  ConnectingLane ::=SEQUENCE {
  lane LaneID,
  -- Index of the connecting lane 
  
  maneuver AllowedManeuvers OPTIONAL
  -- The Maneuver between 
  -- the enclosing lane and this lane
  --at the stop line to connect them
  }
  ```

  lane LaneID车道ID

  ```ASN.1
  【定义】
  定义车道ID。每一条有向路段上的每个车道，都拥有一个单独的ID。数值0表示无效ID。
  【ASN.1 代码】
  LaneID ::= INTEGER (0..255)
  -- the value 0 shall be used when the lane ID is
  -- not available or not known
  -- the value 255 is reserved for future use
  ```

  maneuver AllowedManeuvers OPTIONAL车道的允许转向行为

  ```ASN.1
  【定义】
  定义一个（机动车）车道的允许转向行为。
  【ASN.1 代码】
  AllowedManeuvers ::= BIT STRING {
  --With bits as defined:
  --Allowed maneuvers at path end (stop line)
  --All maneuvers with bits not set are therefore prohibited
  --A value of zero shall be used for unknown,indicating no Maneuver 
  maneuverStraightAllowed (0),
  --a Straight movement is allowed in this lane 
  maneuverLeftAllowed (1),
  --a Left Turn movement is allowed in this lane 
  maneuverRightAllowed (2),
  --a Right Tum movement is allowed in this lane 
  maneuverUTurnAllowed (3),
  --a U turn movement is allowed in this lane 
  maneuverLeftTurnOnRedAllowed (4),
  --a Stop, and then proceed when safe movement
  --is allowed in this lane
  maneuverRightTurnOnRedAllowed (5),
  --a Stop, and then proceed when safe movement
  --is allowed in this lane 
  maneuverLaneChangeAllowed (6),
  --a movement which changes to an outer lane
  --on the egress side is allowed in this lane
  --(example: left into either outbound lane) 
  maneuverNoStoppingAllowed (7),
  --the vehicle should not stop at the stop line
  --(example: a flashing green arrow) 
  yieldAllwaysRequired (8),
  --the allowed movements above are not protected
  --(example: an permanent yellow condition) 
  goWithHalt (9),
  --after making a full stop, may proceed 
  caution (10),
  --proceed past stop line with caution 
  reserved1 (11)
  --used to align to12 Bit Field
  } (SIZE(12))
  ```


phaseId相位 ID

```ASN.1
【定义】
定义信号灯相位 ID。数值o表示无效ID。
【ASN.1 代码】
PhaseID ::= INTEGER (0..255)
--The value 0 shall be used when the ID is not available or not known
```