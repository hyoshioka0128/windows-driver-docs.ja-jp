---
title: Windows カーネルモード セキュリティ リファレンス モニター
description: Windows カーネルモード セキュリティ リファレンス モニター
ms.assetid: 80c63d9c-cb8e-47c0-8afd-ca78dbc43327
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 448bdab0b8278cb5816d60b24d1d9437994bc45c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379354"
---
# <a name="windows-kernel-mode-security-reference-monitor"></a>Windows カーネルモード セキュリティ リファレンス モニター


オペレーティング システムのますます重要な側面にはセキュリティです。 アクションを配置する前に、オペレーティング システムは、アクションはシステム ポリシーに違反ではないことを確認である必要があります。 たとえば、デバイスは可能性があります。 またはすべての要求にアクセスできない可能性があります。 ドライバーを作成するときに、成功し、失敗すると、要求を行うエンティティのアクセス許可に応じていくつかの要求を許可したい場合があります。

Windows では、どのオブジェクトがどのようなセキュリティを判断するのにアクセス制御リスト (ACL) を使用します。 Windows カーネル モードのセキュリティ参照モニターは、アクセス制御を使用するドライバーのルーチンを提供します。 ACL の詳細については、次を参照してください。[アクセス制御リスト](https://msdn.microsoft.com/library/windows/hardware/ff538821)します。

セキュリティ参照モニターを直接インターフェイスを提供するルーチンには、文字のプレフィックス"**Se**"。 たとえば、 **SeAccessCheck**します。 セキュリティの参照の監視ルーチンの一覧は、次を参照してください。[セキュリティ参照モニター ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff563711)します。

 

 




