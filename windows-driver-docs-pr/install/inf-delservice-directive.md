---
title: INF DelService ディレクティブ
description: 1つ以上の以前にインストールされたデバイス/ドライバーサービスを対象のコンピューターから削除するには、DDInstall. Services セクションで DelService ディレクティブを使用します。
ms.assetid: eca57f7c-1551-4247-ab1f-858e6e3ad9d7
keywords:
- INF DelService ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f64f6ed464c29e6977965d0254399851d316c74
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223180"
---
# <a name="inf-delservice-directive"></a>INF DelService ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Delservice**ディレクティブは、 [ *ddinstall * で使用されます。[サービス](inf-ddinstall-services-section.md)] セクションで、以前にインストールされた1つまたは複数のデバイス/ドライバーサービスをターゲットコンピューターから削除します。

```inf
[DDInstall.Services] 
 
DelService=ServiceName[,[flags][,[EventLogType][,EventName]]
...
```

## <a name="entries"></a>エントリ


<a href="" id="servicename"></a>*ServiceName*  
削除するサービスの名前を指定します。

デバイスの場合、この値は通常、"sermouse" やそのような名前のように、ドライバーの汎用的な名前になります。

<a href="" id="flags"></a>*示す*  
この省略可能な値は、次の1つ以上のフラグを指定し*ます。* これは、次のように、setupapi.log で定義され、16進数の値として指定します。

<a href="" id="0x00000004--spsvcinst-deleteeventlogentry-"></a>**0x00000004** (SPSVCINST_DELETEEVENTLOGENTRY)  
指定した ServiceName に関連付けられているイベントログエントリ (またはエントリ) もシステムから削除する必要があります。

<a href="" id="0x00000200---spsvcinst-stopservice--"></a>**0x00000200** (SPSVCINST_STOPSERVICE)   
サービスを削除する前に停止してください。

<a href="" id="eventlogtype"></a>*EventLogType*  
オプションで、**システム**、**セキュリティ**、または**アプリケーション**のいずれかを指定します。 削除するイベントログの種類が**システム**の場合は、この設定を省略できます。

<a href="" id="eventname"></a>*EventName*  
必要に応じて、イベントログの名前を指定します。 指定した*ServiceName*エントリと同じ場合は、省略できます。

<a name="remarks"></a>解説
-------

このディレクティブはほとんど使用されません。 安全に削除できるサービスは、以前のバージョンのオペレーティングシステムでのみ使用されていたものであり、現在インストールされているバージョンでは使用されません。

Windows XP 以降では、 *TargetOSVersion*デコレーションを使用して、バージョン固有のインストール動作を制御できます。 この装飾の詳細については、「 [**INF Manufacturer」セクション**](inf-manufacturer-section.md)を参照してください。

ただし、既定では、特定のデバイスドライバーによって提供されるイベントログ情報は、ドライバーサービスの削除と共にイベントログの削除 (*flags*または*EventName*) を明示的に要求しない限り、アンインストール時にシステムから削除されません。

## <a name="see-also"></a>関連項目


[**AddService**](inf-addservice-directive.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






