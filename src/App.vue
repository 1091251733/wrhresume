<template>
  <div class="relative min-h-screen">
    <!-- 背景粒子装饰 -->
    <div class="bg-particles hidden md:block">
      <span></span><span></span><span></span><span></span> <span></span
      ><span></span><span></span><span></span>
    </div>

    <!-- 主内容 -->
    <div
      class="relative z-10 w-full max-w-[720px] mx-auto px-4 pb-16 pt-6 md:pt-10"
    >
      <!-- ===== 头像 + 姓名 + 职位 ===== -->
      <div class="flex flex-col items-center mb-8">
        <div class="avatar-ring mb-5">
          <div
            class="w-[110px] h-[110px] md:w-[130px] md:h-[130px] rounded-full overflow-hidden bg-gradient-to-br from-purple-200 via-pink-100 to-amber-100 flex items-center justify-center shadow-lg"
          >
            <span
              class="text-4xl md:text-5xl font-bold gradient-text select-none"
              >{{ userInfo.name.charAt(0) }}</span
            >
          </div>
        </div>
        <h1
          class="hero-enter text-3xl md:text-4xl font-extrabold tracking-wide mb-2"
        >
          {{ userInfo.name }}
        </h1>
        <p class="hero-enter text-base text-slate-500 tracking-widest">
          {{ userInfo.job }}
        </p>
      </div>

      <!-- ===== 基本信息 ===== -->
      <div ref="section1" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">基本信息</span>
        </div>
        <div class="flex flex-wrap gap-2">
          <span
            v-for="(item, i) in userInfo.infoList"
            :key="i"
            class="info-tag"
          >
            <span class="text-slate-400">{{ item.label }}</span>
            <span class="text-slate-700 font-medium">{{ item.value }}</span>
          </span>
        </div>
      </div>

      <!-- ===== 求职意向 ===== -->
      <div ref="section2" class="scroll-reveal mb-5">
        <div class="intent-card">
          <div class="flex items-center gap-2">
            <span class="text-2xl">🎯</span>
            <div>
              <div class="text-xs text-slate-400">期望职位</div>
              <div class="font-bold text-slate-800">
                {{ userInfo.jobIntention.position }}
              </div>
            </div>
          </div>
          <div class="w-px h-10 bg-purple-200 hidden sm:block"></div>
          <div class="flex items-center gap-2">
            <span class="text-2xl">💰</span>
            <div>
              <div class="text-xs text-slate-400">期望薪资</div>
              <div class="font-bold text-purple-600">
                {{ userInfo.jobIntention.salary }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- ===== 教育背景 ===== -->
      <div ref="section3" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">教育背景</span>
        </div>
        <div class="timeline">
          <div
            v-for="(edu, i) in userInfo.educationList"
            :key="i"
            class="timeline-item"
          >
            <div class="flex justify-between items-start flex-wrap gap-1">
              <span class="font-bold text-slate-800">{{ edu.school }}</span>
              <span
                class="text-xs text-purple-500 font-medium whitespace-nowrap"
                >{{ edu.period }}</span
              >
            </div>
            <div class="text-sm text-slate-500 mt-0.5">{{ edu.major }}</div>
            <div
              v-if="edu.courses"
              class="text-xs text-slate-400 mt-1 leading-relaxed"
            >
              {{ edu.courses }}
            </div>
          </div>
        </div>
      </div>

      <!-- ===== 在校经历 ===== -->
      <div ref="section4" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">在校经历</span>
        </div>
        <div class="flex justify-between items-start flex-wrap gap-1 mb-3">
          <span class="font-bold text-slate-800">{{
            userInfo.campusExperience.role
          }}</span>
          <span class="text-xs text-purple-500 font-medium whitespace-nowrap">{{
            userInfo.campusExperience.period
          }}</span>
        </div>
        <ul class="space-y-1.5">
          <li
            v-for="(item, i) in userInfo.campusExperience.items"
            :key="i"
            class="text-sm text-slate-600 flex gap-2"
          >
            <span class="text-purple-400 flex-shrink-0 mt-0.5">✦</span>
            <span>{{ item }}</span>
          </li>
        </ul>
      </div>

      <!-- ===== 实习经历 ===== -->
      <div ref="section5" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">实习经历</span>
        </div>
        <div class="flex justify-between items-start flex-wrap gap-1 mb-2">
          <span class="font-bold text-slate-800">{{
            userInfo.internship.company
          }}</span>
          <span class="text-xs text-purple-500 font-medium whitespace-nowrap">{{
            userInfo.internship.period
          }}</span>
        </div>
        <div class="flex items-center gap-2 mb-2">
          <span
            class="text-xs bg-purple-100 text-purple-600 px-2.5 py-0.5 rounded-full"
            >{{ userInfo.internship.role }}</span
          >
        </div>
        <p class="text-sm text-slate-500 leading-relaxed">
          {{ userInfo.internship.description }}
        </p>
      </div>

      <!-- ===== 工作经历 ===== -->
      <div ref="section6" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">工作经历</span>
        </div>
        <div
          v-for="(job, i) in userInfo.employmentList"
          :key="i"
          class="timeline-item"
        >
          <div class="flex justify-between items-start flex-wrap gap-1 mb-1">
            <span class="font-bold text-slate-800">{{ job.company }}</span>
            <span
              class="text-xs text-purple-500 font-medium whitespace-nowrap"
              >{{ job.period }}</span
            >
          </div>
          <span
            class="text-xs bg-purple-100 text-purple-600 px-2.5 py-0.5 rounded-full inline-block mb-3"
            >{{ job.role }}</span
          >
          <div v-for="(h, j) in job.highlights" :key="j" class="mb-3 last:mb-0">
            <div
              class="text-sm font-semibold text-slate-700 mb-1 flex items-center gap-1.5"
            >
              <span
                class="w-1.5 h-1.5 rounded-full bg-purple-400 flex-shrink-0"
              ></span>
              {{ h.title }}
            </div>
            <p class="text-sm text-slate-500 leading-relaxed pl-4">
              {{ h.detail }}
            </p>
          </div>
        </div>
      </div>

      <!-- ===== 技能特长 ===== -->
      <div ref="section7" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">技能特长</span>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-6 gap-y-3">
          <div v-for="(skill, i) in userInfo.skillExpertise" :key="i">
            <div class="flex justify-between items-center mb-1">
              <span class="text-sm font-medium text-slate-700">{{
                skill.name
              }}</span>
              <span class="text-xs text-purple-500">{{ skill.level }}%</span>
            </div>
            <div class="skill-bar">
              <div class="skill-bar-fill" :data-level="skill.level"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- ===== 项目经历 ===== -->
      <div ref="section8" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">项目经历</span>
        </div>
        <div
          v-for="(proj, i) in userInfo.projectExperienceList"
          :key="i"
          class="mb-4 last:mb-0"
        >
          <div class="flex justify-between items-start flex-wrap gap-1 mb-1">
            <span class="font-bold text-slate-800 text-base">{{
              proj.project
            }}</span>
            <span
              class="text-xs text-purple-500 font-medium whitespace-nowrap"
              >{{ proj.period }}</span
            >
          </div>
          <span
            class="text-xs bg-amber-100 text-amber-700 px-2.5 py-0.5 rounded-full inline-block mb-2"
            >{{ proj.role }}</span
          >
          <p class="text-sm text-slate-500 leading-relaxed mb-3">
            {{ proj.summary }}
          </p>
          <div class="text-xs text-slate-400 mb-2">
            <span class="font-semibold text-slate-500">技术栈：</span
            >{{ proj.techStack }}
          </div>
          <div class="text-sm text-slate-500 space-y-1">
            <div v-for="(d, j) in proj.dutiesList" :key="j" class="flex gap-2">
              <span class="text-purple-400 flex-shrink-0 mt-0.5">✦</span>
              <span>{{ d }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- ===== 奖项荣誉 ===== -->
      <div ref="section9" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">证书荣誉</span>
        </div>
        <div class="flex flex-wrap gap-2">
          <span
            v-for="(award, i) in userInfo.awardsList"
            :key="i"
            class="award-badge"
          >
            <span>🏅</span>
            <span>{{ award }}</span>
          </span>
        </div>
        <br />
        <NCarousel
          v-if="userInfo.imageList?.length"
          show-arrow
          draggable
          mousewheel
        >
          <NImage
            class="w-full !h-[520px] rounded-md"
            v-for="(url, i) in userInfo.imageList"
            :key="i"
            :src="getImageUrl(url)"
            :data-local="getLocalUrl(url)"
            @error="handleImageError"
            lazy
          />
        </NCarousel>
      </div>

      <!-- ===== 自我评价 ===== -->
      <div ref="section10" class="scroll-reveal glass-card p-5 mb-5">
        <div class="section-title">
          <span class="icon-dot"></span>
          <span class="gradient-text">自我评价</span>
        </div>
        <div class="quote-block mb-4">
          <p class="text-sm leading-relaxed">
            {{ userInfo.selfEvaluation.summary }}
          </p>
        </div>
        <div
          v-for="(hl, i) in userInfo.selfEvaluation.highlights"
          :key="i"
          class="mb-4 last:mb-3"
        >
          <div class="flex items-center gap-2 mb-1.5">
            <span class="text-lg">{{
              i === 0 ? "📋" : i === 1 ? "📊" : "🤝"
            }}</span>
            <span class="font-bold text-slate-700 text-sm">{{ hl.title }}</span>
          </div>
          <p class="text-sm text-slate-500 leading-relaxed pl-7">
            {{ hl.detail }}
          </p>
        </div>
        <div class="mt-4 pt-3 border-t border-purple-100">
          <p class="text-sm text-slate-500 italic text-center leading-relaxed">
            {{ userInfo.selfEvaluation.closing }}
          </p>
        </div>
      </div>

      <!-- 底部水波纹装饰 -->
      <div class="wave-divider">
        <svg viewBox="0 0 120 120" preserveAspectRatio="none">
          <path
            d="M0,40 C200,80 400,0 600,40 C800,80 100,0 120,40 L120,120 L0,120 Z"
            fill="rgba(192,132,252,0.08)"
          ></path>
          <path
            d="M0,60 C200,100 400,20 600,60 C800,100 100,20 120,60 L120,120 L0,120 Z"
            fill="rgba(244,114,182,0.06)"
          ></path>
        </svg>
      </div>

      <!-- 底部签名 -->
      <div class="text-center text-xs text-slate-300 mt-4 pb-4">
        {{ userInfo.name }} · {{ userInfo.job }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { NCarousel, NImage } from "naive-ui";
import { onMounted, onUnmounted, ref } from "vue";
import { userInfo } from "./store/tableDate";

// 所有 section 的 ref
const section1 = ref(null);
const section2 = ref(null);
const section3 = ref(null);
const section4 = ref(null);
const section5 = ref(null);
const section6 = ref(null);
const section7 = ref(null);
const section8 = ref(null);
const section9 = ref(null);
const section10 = ref(null);

// Intersection Observer：滚动入场动画 + 技能条动画
let observer = null;

/** 解析图片 URL：cdn 地址优先，否则用本地路径 */
function getImageUrl(url) {
  if (typeof url === "string") {
    return url;
  }
  if (url?.cdn && /^https?:\/\//.test(url.cdn)) {
    return url.cdn;
  }
  if (url?.local) {
    return new URL(url.local, import.meta.url).href;
  }
  return "";
}

/** 始终返回本地图片的 Vite 解析后地址（用于 cdn 失败后的兜底） */
function getLocalUrl(url) {
  if (url?.local) {
    return new URL(url.local, import.meta.url).href;
  }
  return typeof url === "string" ? url : "";
}

/** NImage @error 回调：cdn 加载失败时自动切换到本地图片 */
const handleImageError = (event) => {
  const img = event.target;
  // 已回退过本地图片就不再重试，防止死循环
  if (img.dataset.fallback === "1") return;
  const localUrl = img.dataset.local;
  if (localUrl) {
    img.dataset.fallback = "1";
    img.src = localUrl;
  }
};
onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("visible");

          // 技能条动画：当技能区域进入视口时触发
          const skillBars = entry.target.querySelectorAll(".skill-bar-fill");
          skillBars.forEach((bar) => {
            const level = bar.getAttribute("data-level");
            if (level) {
              setTimeout(() => {
                bar.style.width = level + "%";
              }, 200);
            }
          });
        }
      });
    },
    { threshold: 0.15, rootMargin: "0px 0px -40px 0px" },
  );

  // 观察所有 section
  const sections = [
    section1,
    section2,
    section3,
    section4,
    section5,
    section6,
    section7,
    section8,
    section9,
    section10,
  ];
  sections.forEach((s) => {
    if (s.value) observer.observe(s.value);
  });
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>
