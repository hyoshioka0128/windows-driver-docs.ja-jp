---
title: INF SharedDriver エントリ
description: INF SharedDriver エントリ
ms.assetid: 36d094b4-481d-41bb-b034-345b0743456e
keywords:
- INF ファイル WDK 非 HID キーボード/マウス
- SharedDriver エントリ WDK 非 HID キーボード/マウス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e310ae8ba831d3577ba55c52c2b3bda2df8d800
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363548"
---
# <a name="inf-shareddriver-entry"></a>INF SharedDriver エントリ





**\[ControlFlags\]**

<em>SharedDriver</em> **=** <em>インストール セクション名</em>***、***<em>警告文字列</em>キーボードの前にps/2 デバイスをインストールすると、マウス クラスのインストーラーをチェックまたは、 *SharedDriver*内のエントリ、 [INF **ControlFlags**セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)デバイス。 このようなエントリの値が存在する場合、クラスのインストーラーは、警告のテキスト文字列を表示することで、ユーザーに通知し、ユーザー ps/2 ポート ドライバーの変更をキャンセルするオプションを提供します。

### <a name="entries-and-values"></a>エントリと値

<a href="" id="shareddriver"></a>*SharedDriver*  
デバイス ドライバーが両方 ps/2 キーボードとマウス デバイスで共有されることを指定します。

<a href="" id="install-section-name"></a>*install-section-name*  
デバイスの指定*DDInstall*セクション。

<a href="" id="warning-text-string"></a>*警告テキスト文字列*  
クラスのインストーラーは、ps/2 ポート ドライバーを変更する前に、ユーザーに警告を使用して文字列を指定します。

 

 




