---
title: INF DelService ディレクティブ
description: 対象のコンピューターからの詳細は以前インストールされているデバイス ドライバー/サービスまたは DelService ディレクティブは、1 つを削除する DDInstall.Services セクションで使用されます。
ms.assetid: eca57f7c-1551-4247-ab1f-858e6e3ad9d7
keywords:
- INF DelService ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7b0d1a47050af081d57ee2c9c6947bccbf49658
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577837"
---
# <a name="inf-delservice-directive"></a>INF DelService ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **DelService**にディレクティブを使用する[ * **DDInstall *。サービス**](inf-ddinstall-services-section.md)セクションを 1 つを削除または、対象コンピュータからの詳細は以前インストールされているデバイス ドライバー/サービス。

```ini
[DDInstall.Services] 
 
DelService=ServiceName[,[flags][,[EventLogType][,EventName]]
...
```

## <a name="entries"></a>エントリ


<a href="" id="servicename"></a>*サービス名*  
削除するサービスの名前を指定します。

この値はデバイスの場合は"sermouse、"など、そのドライバーの汎用的な名前またはそのようないくつかの名前は、通常です。

<a href="" id="flags"></a>*フラグ*  
この省略可能な値は 1 つまたは複数の定義で、次のフラグを指定します*Setupapi.h*、16 進数の値として指定されています。

<a href="" id="0x00000004--spsvcinst-deleteeventlogentry-"></a>**0x00000004** (SPSVCINST_DELETEEVENTLOGENTRY)  
イベント ログ、システムから特定のサービス名に関連付けられているエントリ (またはエントリ) を削除するかもします。

<a href="" id="0x00000200---spsvcinst-stopservice--"></a>**0x00000200** (SPSVCINST_STOPSERVICE)   
削除する前に、サービスを停止します。

<a href="" id="eventlogtype"></a>*EventLogType*  
必要に応じてのいずれかを指定します。**システム**、**セキュリティ**、または**アプリケーション**します。 削除するイベント ログは、型の場合は省略可能この**システム**します。

<a href="" id="eventname"></a>*eventName*  
必要に応じて、イベント ログの名前を指定します。 指定したのと同じ場合は省略可能この*ServiceName*エントリ。

<a name="remarks"></a>コメント
-------

このディレクティブはほとんど使用されません。 安全に削除できる唯一のサービスはいるか、オペレーティング システムの以前のバージョンでのみ使用され、現在のバージョンで使用されないためです。

使用できます Windows XP 以降、 *TargetOSVersion*コントロール バージョン固有のインストール時の動作を装飾します。 この装飾の詳細については、次を参照してください。 [ **INF 製造元セクション**](inf-manufacturer-section.md)します。

ただし、既定では、特定のデバイス ドライバーが提供するイベント ログ情報は削除されません、アンインストール、システムから、デバイスとドライバーの INF が明示的に削除を要求しない限り (*フラグ*または*EventName*) ドライバー サービスの削除と共にイベント ログの。

## <a name="see-also"></a>関連項目


[**AddService**](inf-addservice-directive.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






