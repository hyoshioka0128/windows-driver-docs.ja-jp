---
title: MALT のマイクロ コント ローラー コマンド
author: windows-driver-content
description: このトピックでは、PC と、MALT のセンサーを制御するマイクロ (Arduino) の間のコマンドを定義します。
ms.assetid: 38b9c6fc-f13c-4af5-90ab-d9931dc9b7f1
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6e73d78f584724d27ed882cccfa632501fdf2c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560473"
---
# <a name="microcontroller-commands-for-malt"></a>MALT のマイクロ コント ローラー コマンド

このトピックでは、PC と、MALT のセンサーを制御するマイクロ (Arduino) の間のコマンドを定義します。 マイクロ コント ローラーを制御する PC に、システムまたはテスト (SUT/DUT) 対象のデバイスもことをお勧めします。  

## <a name="serial-command-interface"></a>シリアル コマンド インターフェイス

次のシリアル コマンドを使用してリモート テスト マシン群と通信します。 各コマンドはへの書き込みし、一連の行の間のシリアルから読み取る。


### <a name="light-light-level"></a>LIGHT*ライト レベル*

指定した入力に基づいて光のレベルを調整します。

[ライト パネル](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/).25 と 1.3 の間の参照をサポートで使用される入力のボルト。

DAC のリファレンス データ シートを使用して[マイクロ チップ MCP4821](https://www.microchip.com/wwwproducts/en/MCP4821)、最大値に解決できます*Vout*ライトのパネルに送信します。

1.3 = 2.048 * 1 * (D/(2^12))

D = 2600

**例:** 

次の例では、(上の数式に基づく)、最大輝度に光を取得するために必要な電圧を送信します。

```cmd
LIGHT 2600
```



**シリアル出力:**

| 行 0                |
|-----------------------|
| MALTERROR 状態コード |

### <a name="readalssensor-sensor-number"></a>READALSSENSOR*センサーの数*

センサーの数値の定義は次のとおりです。

1. 環境光センサーが (画面から離れた場所に接続する)
2. 画面の光センサー (画面方向を向き)

**例:**

次の例では、シリアル画面光センサーから、結果の生データを書き込みます。 Lux をに基づいて計算することができます、[データシート](https://www.ti.com/product/OPT3001)のセンサーを使用します。

```cmd
READALSSENSOR 2
```

**シリアル出力:**

| 行 0                | 1 行目                  | 2 行目                |
|-----------------------|-------------------------|-----------------------|
| MALTERROR 状態コード | 指数 (失敗した場合は 0) | 結果 (0 を返します) |

### <a name="readcolorsensor-sensor-number"></a>READCOLORSENSOR*センサーの数*

センサーの数値の定義は次のとおりです。

1. アンビエントの色センサー (画面から離れた場所に接続する)
2. 画面の色のセンサー (画面方向を向き)

**例:**

次の例では、シリアル、画面の色のセンサーから、結果の生データを書き込みます。 Lux をに基づいて計算することができます、[データシート](https://www.ti.com/product/OPT3001)のセンサーを使用します。

```cmd
READCOLORSENSOR 2
```

**シリアル出力:**

| 行 0                | 1 行目    | 2 行目      | 3 行目     |
|-----------------------|-----------|-------------|------------|
| MALTERROR 状態コード | 赤の値 | 緑の値 | 青の値 |

### <a name="conversiontime-conversion-time-in-ms"></a>CONVERSIONTIME*変換時間 (ミリ秒)*

[OPT3001](https://www.ti.com/product/OPT3001)参照で使用される光センサーは、変換の 2 倍をサポートします。値と 100 ミリ秒です。
CONVERSIONTIME では、両方のセンサーの変換にかかる時間を変更します。

> [!NOTE] 
> 測定変換が進行中の場合、構成のレジスタが書き込まれるときに、アクティブな測定値の変換がすぐに中止されます。

**例:** 

次の例では、両方のセンサーの変換にかかる時間を 100 ミリ秒に変更します。

MALT プロトタイプで使用される既定変換にかかる時間は、値です。

```cmd
CONVERSIONTIME 100
```

**シリアル出力:**

| 行 0                |
|-----------------------|
| MALTERROR 状態コード |

### <a name="unrecognized-commands"></a>認識できないコマンド

いずれかのコマンドを認識できません。 

**シリアル出力:**

| 行 0                |
|-----------------------|
| MALTERROR 状態コード |

場所 MALTERROR 状態コード = `E_UNRECOGNIZED_COMMAND`

## <a name="malt-error-code"></a>MALT エラー コード

| E_SUCCESS | E_INVALID_PARAM | E_UNRECOGNIZED_COMMAND |
|-----------| --------------- | ---------------------- |
| 0         | 1               | 2                      |