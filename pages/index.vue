<template>
    <div class="flex flex-wrap justify-center">
        <ElSteps
            direction="vertical"
            align-center
            space="12vh"
            class="mt-5 w-full !flex-wrap content-center"
        >
            <ElStep
                v-for="(activity, index) in activities"
                :key="index"
                :status="style(activity.start, activity.finish)"
                class="tracking-[1.5px]"
            >
                <template #title>
                    <div class="font-bold sm:text-lg">
                        {{ activity.content }}
                    </div>
                </template>
                <template #description>
                    <div class="min-w-max sm:text-base">
                        {{
                            activity.start.toLocaleString(undefined, {
                                dateStyle: 'long',
                            }) +
                            (activity.end
                                ? '〜' +
                                  activity.end.toLocaleString(undefined, {
                                      dateStyle: 'long',
                                  })
                                : '')
                        }}
                        {{ activity.maybe ? '(預定)' : '' }}
                    </div>
                </template>
            </ElStep>
        </ElSteps>
        <ElButton
            v-if="status === 'authenticated'"
            type="success"
            class="my-5 animate-bounce hover:animate-none"
            @click="useRouter().push('/vote')"
        >
            <span class="font-bold">前 往 投 票 頁 面</span>
        </ElButton>
        <ElButton
            v-else
            type="primary"
            class="my-5 animate-bounce hover:animate-none"
            @click="useRouter().push('/login')"
        >
            <span class="font-bold">前 往 登 入 頁 面</span>
        </ElButton>
    </div>
</template>

<script setup lang="ts">
definePageMeta({
    auth: false,
    title: '首頁',
})

const { status } = useAuth()

const style = (start: Date, end: Date) => {
    return Date.now() < start.getTime()
        ? 'process'
        : Date.now() < end.getTime()
        ? 'finish'
        : 'success'
}

const activities = [
    {
        content: '登記參選',
        start: new Date(2024, 4, 1),
        end: new Date(2024, 4, 12),
        finish: new Date(2024, 4, 13),
        maybe: false,
    },
    {
        content: '候選人名單公告',
        start: new Date(2024, 4, 15),
        finish: new Date(2024, 4, 16),
        maybe: false,
    },
    {
        content: '選舉公報',
        start: new Date(2024, 4, 17),
        finish: new Date(2024, 4, 18),
        maybe: false,
    },
    {
        content: '候選人政見發表會',
        start: new Date(2023, 4, 22),
        finish: new Date(2023, 4, 23),
        maybe: false,
    },
    {
        content: '線上投票',
        start: new Date(2024, 4, 24),
        finish: new Date(2024, 4, 25),
        maybe: false,
    },
    {
        content: '當選名單公告',
        start: new Date(2023, 4, 25),
        finish: new Date(2023, 4, 26),
        maybe: false,
    },
    {
        content: '(補選)登記參選',
        start: new Date(2023, 4, 26),
        end: new Date(2023, 5, 1),
        finish: new Date(2023, 5, 2),
        maybe: false,
    },
    {
        content: '(補選)候選人名單公告 + 選舉公報',
        start: new Date(2023, 5, 3),
        finish: new Date(2023, 5, 4),
        maybe: false,
    },
    {
        content: '(補選)線上投票',
        start: new Date(2023, 5, 12),
        finish: new Date(2023, 5, 13),
        maybe: false,
    },
    {
        content: '(補選)當選名單公告',
        start: new Date(2023, 5, 13),
        finish: new Date(2023, 5, 14),
        maybe: false,
    },
]
</script>




