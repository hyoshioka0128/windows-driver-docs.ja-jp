---
title: メンテナンス
description: メンテナンス
ms.assetid: 228759ed-f6de-4680-adf2-ca88b83ff4a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e2c387c5d20d4233ae63f13b192180d85d15b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572268"
---
# <a name="maintenance"></a>メンテナンス


スキーマのパス:\\Printer.Maintenance

ノード型: プロパティ

メンテナンス プロパティには、印刷デバイスのメンテナンスに関する情報が含まれています。

メンテナンス プロパティには、2 つの子の値が含まれています。**AlignHead**と**CleanHead**します。

### <a name="span-idalignheadspanspan-idalignheadspan-alignhead"></a><span id="alignhead"></span><span id="ALIGNHEAD"></span> AlignHead

スキーマのパス:\\Printer.Maintenance.AlignHead

ノードの種類:[値]

［データの種類］:BIDI\_BOOL

説明:この値は、デバイスで、ヘッドの配置手順を実行するコマンドを表します。 この値は、書き込み専用値です。 この値を読み取ることを拒否する必要があります。 値が 1 に設定されている場合、デバイスは、コマンドを実行する必要があります。

### <a name="span-idcleanheadspanspan-idcleanheadspan-cleanhead"></a><span id="cleanhead"></span><span id="CLEANHEAD"></span> CleanHead

スキーマのパス:\\Printer.Maintenance.CleanHead

ノードの種類:[値]

［データの種類］:BIDI\_BOOL

説明:この値は、[ヘッド クリーニング] デバイス上の手順を実行するコマンドを表します。 この値は、書き込み専用値です。 この値を読み取ることを拒否する必要があります。 値が 1 に設定されている場合、デバイスは、コマンドを実行する必要があります。

 

 




