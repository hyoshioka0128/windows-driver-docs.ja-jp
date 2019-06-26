---
title: オーディオ アダプターのバージョン情報の指定
description: オーディオ アダプターのバージョン情報の指定
ms.assetid: 2d1fb5e7-84fe-451f-b53f-bf6017ae94ad
keywords:
- オーディオ アダプター WDK、バージョン情報
- アダプターのドライバー WDK オーディオ、バージョン情報
- ポート クラス オーディオ アダプター WDK、バージョン情報
- バージョンの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5cd4405c69a99679194c144b2a5684c29877f24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354286"
---
# <a name="specifying-version-information-for-an-audio-adapter"></a>オーディオ アダプターのバージョン情報の指定


## <span id="specifying_version_information_for_an_audio_adapter"></span><span id="SPECIFYING_VERSION_INFORMATION_FOR_AN_AUDIO_ADAPTER"></span>


仕入先に次のエントリを指定する必要があります、**バージョン**ポート クラス オーディオ アダプターの INF ファイルのセクション。

```inf
  Signature="$CHICAGO$"
  Class=MEDIA
  ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
```

すべてのデバイス クラスの追加のバージョン要件およびオプションの説明は、次を参照してください。 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)します。

 

 




