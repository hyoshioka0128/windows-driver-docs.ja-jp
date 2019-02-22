---
title: オーディオのアダプターのバージョン情報を指定します。
description: オーディオのアダプターのバージョン情報を指定します。
ms.assetid: 2d1fb5e7-84fe-451f-b53f-bf6017ae94ad
keywords:
- オーディオ アダプター WDK、バージョン情報
- アダプターのドライバー WDK オーディオ、バージョン情報
- ポート クラス オーディオ アダプター WDK、バージョン情報
- バージョンの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f79b19799bbb1aa8c4def21888b97c31d6ad769b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552827"
---
# <a name="specifying-version-information-for-an-audio-adapter"></a>オーディオのアダプターのバージョン情報を指定します。


## <span id="specifying_version_information_for_an_audio_adapter"></span><span id="SPECIFYING_VERSION_INFORMATION_FOR_AN_AUDIO_ADAPTER"></span>


仕入先に次のエントリを指定する必要があります、**バージョン**ポート クラス オーディオ アダプターの INF ファイルのセクション。

```inf
  Signature="$CHICAGO$"
  Class=MEDIA
  ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
```

すべてのデバイス クラスの追加のバージョン要件およびオプションの説明は、次を参照してください。 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)します。

 

 




