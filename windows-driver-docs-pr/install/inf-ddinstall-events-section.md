---
title: INF DDInstall.Events セクション
author: andylsn
description: 各モデルあたり DDInstall.Events セクションには、INF ファイルに追加の INF ライター定義セクションを参照する 1 つまたは複数の INF AddEventProvider ディレクティブが含まれています。
ms.assetid: ''
keywords:
- INF DDInstall.Events セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Events Section
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f46a416ceb244e5532115b9666e4586899f3c41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574036"
---
# <a name="inf-ddinstallevents-section"></a>INF DDInstall.Events セクション

各ごとのモデル<em>DDInstall</em>**します。イベント**セクションは、1 つ以上含まれています。 [ **INF AddEventProvider ディレクティブ**](inf-addeventprovider-directive.md) INF ライター定義の追加のセクションで、INF ファイルを参照します。 このセクションでは、Windows 10 は 1809 およびそれ以降のバージョンでサポートされます。

```ini
[install-section-name.Events] |
[install-section-name.nt.Events] |
[install-section-name.ntx86.Events] |
[install-section-name.ntia64.Events] |
[install-section-name.ntamd64.Events] |
[install-section-name.ntarm.Events] |
[install-section-name.ntarm64.Events] |

AddEventProvider={ProviderGUID},event-provider-install-section
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

行うことができます、 <em>DDInstall</em>**します。イベント**に少なくとも 1 つのセクション**AddEventProvider**を登録するディレクティブ[Windows のイベント トレース](https://msdn.microsoft.com/library/windows/desktop/aa363668)(ETW) プロバイダーです。

## <a name="entries"></a>エントリ

<a href="" id="addeventprovider--providerguid--event-provider-install-section"></a>**AddEventProvider=**{*ProviderGUID*},*event-provider-install-section*  
このディレクティブは、INF ライターの定義を参照*イベント プロバイダーのインストール セクション*この対象となるデバイスのドライバーの INF ファイルの他の場所で*DDInstall*セクション。 詳細については、次を参照してください。 [ **INF AddEventProvider ディレクティブ**](inf-addeventprovider-directive.md)します。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイスをインストールするために必要なセクションが含まれているを指定します。 このエントリが指定されている場合、**必要がある**エントリも通常は必要です。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、このデバイスのインストール中に処理する必要があるセクションを指定します。 セクションは、通常、 <em>DDInstall</em>**します。イベント**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。イベント**セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a name="remarks"></a>コメント
-------

<em>DDInstall</em>**します。イベント**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要[ ***DDInstall*** ](inf-ddinstall-section.md)セクション。 たとえば、<em>インストール セクション名</em>**.ntx86**セクションは、対応する必要が<em>インストール セクション名</em>**.ntx86 します。イベント**セクション。

指定した*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。 大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 <em>DDInstall</em>**します。イベント**クロスプラット フォーム対応の INF ファイルでセクション名。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

<a name="examples"></a>使用例
--------

この例では、<em>インストール セクション名</em>**します。イベント**セクションとそのイベントのプロバイダーのインストール-セクションで、INF ファイルでします。

```ini
[Device_Inst.NT.Events]
AddEventProvider={071acb53-ccfb-42e0-9a68-5336b7301507},foo_Event_Provider_Inst
AddEventProvider={6d3fd9ef-bcbb-42d7-9fbd-1bf2d926b394},bar_Event_Provider_Inst

; entries in the following xxx_Inst sections omitted here for brevity,
; but fully specified as the example for the AddEventProvider directive
;
[foo_Event_Provider_Inst]
; ...

[bar_Event_Provider_Inst]
; ...
```

## <a name="see-also"></a>関連項目


[**AddEventProvider**](inf-addeventprovider-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

 

 





