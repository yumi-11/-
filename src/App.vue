<template>
  <div class="flex h-screen bg-slate-50 text-slate-800 font-sans">
    <!-- 1. 左侧边栏 (Sidebar) -->
    <aside class="w-64 bg-white border-r border-slate-200 flex flex-col justify-between p-4">
      <div>
        <!-- 系统 Logo 与标题 -->
        <div class="flex items-center gap-3 px-2 py-3 mb-6">
          <div class="w-9 h-9 bg-blue-600 rounded-lg flex items-center justify-center text-white font-bold text-lg">
            R
          </div>
          <div>
            <h1 class="font-bold text-base leading-tight">秋招工作台</h1>
            <p class="text-xs text-slate-400">RecruitOps Agent</p>
          </div>
        </div>

        <!-- 主导航菜单 -->
        <nav class="space-y-1">
          <button 
            v-for="item in navItems" 
            :key="item.id"
            @click="activeTab = item.id"
            :class="[
              'w-full flex items-center justify-between px-3 py-2.5 rounded-lg text-sm font-medium transition-colors',
              activeTab === item.id ? 'bg-blue-50 text-blue-600' : 'text-slate-600 hover:bg-slate-100'
            ]"
          >
            <div class="flex items-center gap-3">
              <component :is="item.icon" class="w-4 h-4" />
              <span>{{ item.label }}</span>
            </div>
            <span v-if="item.badge" class="text-xs px-2 py-0.5 rounded-full bg-slate-100 text-slate-500">
              {{ item.badge }}
            </span>
          </button>
        </nav>
      </div>

      <!-- 底部用户信息 -->
      <div class="pt-4 border-t border-slate-100 flex items-center gap-3 px-2">
        <div class="w-8 h-8 rounded-full bg-slate-200 flex items-center justify-center font-semibold text-slate-600 text-xs">
          Yumi
        </div>
        <div class="overflow-hidden">
          <p class="text-sm font-medium text-slate-700 truncate">Yumi (27届校招)</p>
          <p class="text-xs text-slate-400 truncate">数据分析 / AI产品 / 财务</p>
        </div>
      </div>
    </aside>

    <!-- 2. 主内容区域 (Main Content Area) -->
    <main class="flex-1 flex flex-col overflow-hidden">
      <!-- 2.1 Tab 1: 校招岗位 (对应第一张图) -->
      <div v-if="activeTab === 'jobs'" class="flex-1 overflow-y-auto p-8">
        <div class="max-w-7xl mx-auto space-y-6">
          <!-- 页面标题 -->
          <div>
            <h2 class="text-2xl font-bold text-slate-900">27届校招岗位</h2>
            <p class="text-sm text-slate-500 mt-1">自动抓取全网校招岗位，智能匹配最佳投递机会</p>
          </div>

          <!-- 顶部分析卡片格 -->
          <div class="grid grid-cols-4 gap-4">
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
              <p class="text-xs font-medium text-slate-500 mb-1">爬取岗位总数</p>
              <h3 class="text-2xl font-bold text-slate-800">13,778</h3>
              <p class="text-xs text-slate-400 mt-2">较昨日 +124</p>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
              <p class="text-xs font-medium text-slate-500 mb-1">高匹配岗位</p>
              <h3 class="text-2xl font-bold text-purple-600">656</h3>
              <p class="text-xs text-slate-400 mt-2">评分 80 分以上</p>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
              <p class="text-xs font-medium text-slate-500 mb-1">精选岗位</p>
              <h3 class="text-2xl font-bold text-emerald-600">1,371</h3>
              <p class="text-xs text-slate-400 mt-2">推荐优先投递</p>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
              <p class="text-xs font-medium text-slate-500 mb-1">待刷新评分</p>
              <h3 class="text-2xl font-bold text-amber-500">0</h3>
              <p class="text-xs text-slate-400 mt-2">任务队列已空</p>
            </div>
          </div>

          <!-- 筛选与搜索工具栏 -->
          <div class="bg-white p-4 rounded-xl border border-slate-200 space-y-3">
            <div class="grid grid-cols-6 gap-3">
              <input 
                type="text" 
                placeholder="搜索公司、岗位或地点..." 
                class="col-span-2 px-3 py-1.5 text-sm border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
              />
              <select class="px-3 py-1.5 text-sm border border-slate-200 rounded-lg bg-white text-slate-600">
                <option>全部公司</option>
                <option>字节跳动</option>
                <option>腾讯</option>
                <option>京东</option>
              </select>
              <select class="px-3 py-1.5 text-sm border border-slate-200 rounded-lg bg-white text-slate-600">
                <option>全部岗位类型</option>
                <option>AI/大模型</option>
                <option>财务/审计</option>
                <option>数据分析</option>
              </select>
              <select class="px-3 py-1.5 text-sm border border-slate-200 rounded-lg bg-white text-slate-600">
                <option>全部平台</option>
                <option>官网</option>
                <option>公众号</option>
              </select>
              <select class="px-3 py-1.5 text-sm border border-slate-200 rounded-lg bg-white text-slate-600">
                <option>匹配度倒序</option>
                <option>发布时间倒序</option>
              </select>
            </div>
          </div>

          <!-- 岗位数据表格 -->
          <div class="bg-white rounded-xl border border-slate-200 overflow-hidden shadow-sm">
            <table class="w-full text-left text-sm text-slate-600">
              <thead class="bg-slate-50 border-b border-slate-200 text-xs text-slate-500 uppercase">
                <tr>
                  <th class="p-4">公司</th>
                  <th class="p-4">岗位名称</th>
                  <th class="p-4">匹配度</th>
                  <th class="p-4">工作地点</th>
                  <th class="p-4">平台</th>
                  <th class="p-4 text-right">操作</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-slate-100">
                <tr v-for="job in jobsList" :key="job.id" class="hover:bg-slate-50">
                  <td class="p-4 font-medium text-slate-900">{{ job.company }}</td>
                  <td class="p-4">
                    <p class="font-medium text-slate-800">{{ job.title }}</p>
                    <p class="text-xs text-slate-400">{{ job.department }}</p>
                  </td>
                  <td class="p-4">
                    <span class="px-2 py-1 rounded text-xs font-semibold bg-emerald-50 text-emerald-600 border border-emerald-200">
                      {{ job.score }}分
                    </span>
                  </td>
                  <td class="p-4 text-slate-500">{{ job.location }}</td>
                  <td class="p-4 text-slate-400">{{ job.platform }}</td>
                  <td class="p-4 text-right space-x-2">
                    <button @click="activeTab = 'assistant'" class="px-2.5 py-1 text-xs bg-blue-50 text-blue-600 rounded hover:bg-blue-100">
                      AI 匹配分析
                    </button>
                    <button class="px-2.5 py-1 text-xs bg-slate-100 text-slate-600 rounded hover:bg-slate-200">
                      记录投递
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- 2.2 Tab 2: 求职助理对话 (对应第二张图) -->
      <div v-if="activeTab === 'assistant'" class="flex-1 flex overflow-hidden">
        <!-- 历史对话列表 -->
        <div class="w-64 border-r border-slate-200 p-4 bg-white flex flex-col justify-between">
          <div class="space-y-3">
            <button class="w-full py-2 px-3 border border-dashed border-slate-300 text-slate-600 rounded-lg text-sm hover:border-blue-500 hover:text-blue-600 flex items-center justify-center gap-2">
              + 发起新对话
            </button>
            <div class="space-y-1">
              <div v-for="chat in chatHistory" :key="chat.id" class="p-2 text-xs rounded-lg hover:bg-slate-100 cursor-pointer text-slate-700 truncate">
                {{ chat.title }}
              </div>
            </div>
          </div>
        </div>

        <!-- 聊天主界面 -->
        <div class="flex-1 flex flex-col bg-slate-50">
          <div class="p-4 border-b border-slate-200 bg-white flex justify-between items-center">
            <div>
              <h3 class="font-semibold text-slate-800 text-sm">求职助理 Agent</h3>
              <p class="text-xs text-slate-400">已关联知识库：个人简历_财务与数据分析.pdf</p>
            </div>
          </div>
          
          <div class="flex-1 overflow-y-auto p-6 space-y-4">
            <div class="bg-blue-50 border border-blue-100 p-4 rounded-xl max-w-2xl text-sm text-slate-700">
              👋 你好！我是你的专属求职 Agent。我可以帮你分析岗位匹配度、优化简历描述、生成面试准备大纲或解析招聘邮件。
            </div>
          </div>

          <!-- 输入框 -->
          <div class="p-4 bg-white border-t border-slate-200">
            <div class="max-w-4xl mx-auto relative">
              <textarea 
                rows="3" 
                placeholder="请询问岗位匹配分析、简历修改建议或面试准备..." 
                class="w-full p-3 pr-20 text-sm border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 resize-none"
              ></textarea>
              <button class="absolute right-3 bottom-3 px-4 py-1.5 bg-blue-600 text-white text-xs font-medium rounded-lg hover:bg-blue-700">
                发送
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- 2.3 Tab 3: 招聘邮箱 (对应第三张图) -->
      <div v-if="activeTab === 'mailbox'" class="flex-1 overflow-y-auto p-8">
        <div class="max-w-6xl mx-auto space-y-6">
          <div class="flex justify-between items-center">
            <div>
              <h2 class="text-2xl font-bold text-slate-900">招聘邮箱</h2>
              <p class="text-sm text-slate-500 mt-1">自动归集招聘邮件，智能提取笔试、面试及宣讲会安排</p>
            </div>
            <button class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-xs font-medium text-slate-600 hover:bg-slate-50 flex items-center gap-2">
              🔄 同步邮件
            </button>
          </div>

          <!-- 邮件分类汇总 -->
          <div class="grid grid-cols-3 gap-4">
            <div class="bg-white p-4 rounded-xl border border-slate-200 text-center">
              <p class="text-xs text-slate-400">收到通知</p>
              <p class="text-xl font-bold text-slate-800 mt-1">39</p>
            </div>
            <div class="bg-white p-4 rounded-xl border border-slate-200 text-center">
              <p class="text-xs text-slate-400">待办笔试/面试</p>
              <p class="text-xl font-bold text-blue-600 mt-1">6</p>
            </div>
            <div class="bg-white p-4 rounded-xl border border-slate-200 text-center">
              <p class="text-xs text-slate-400">已处理</p>
              <p class="text-xl font-bold text-emerald-600 mt-1">33</p>
            </div>
          </div>

          <!-- 邮件列表 -->
          <div class="bg-white rounded-xl border border-slate-200 divide-y divide-slate-100">
            <div v-for="mail in mailList" :key="mail.id" class="p-4 flex items-center justify-between hover:bg-slate-50">
              <div class="space-y-1">
                <div class="flex items-center gap-2">
                  <span class="px-2 py-0.5 text-xs rounded bg-blue-50 text-blue-600 font-medium">{{ mail.tag }}</span>
                  <p class="font-semibold text-slate-800 text-sm">{{ mail.title }}</p>
                </div>
                <p class="text-xs text-slate-400">{{ mail.sender }} · {{ mail.time }}</p>
              </div>
              <div class="flex items-center gap-2">
                <button class="px-3 py-1 text-xs border border-slate-200 rounded text-slate-600 hover:bg-slate-100">查看邮件</button>
                <button class="px-3 py-1 text-xs bg-blue-50 text-blue-600 rounded hover:bg-blue-100">生成关联日程</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- 2.4 Tab 4: 日程安排 (对应第四、五张图) -->
      <div v-if="activeTab === 'schedule'" class="flex-1 overflow-y-auto p-8">
        <div class="max-w-6xl mx-auto space-y-6">
          <div class="flex justify-between items-center">
            <div>
              <h2 class="text-2xl font-bold text-slate-900">日程安排</h2>
              <p class="text-sm text-slate-500 mt-1">由邮件与任务自动生成的笔面试日程</p>
            </div>
            <div class="flex gap-2">
              <button @click="scheduleView = 'list'" :class="['px-3 py-1.5 text-xs rounded-lg font-medium', scheduleView === 'list' ? 'bg-blue-600 text-white' : 'bg-white border text-slate-600']">列表视图</button>
              <button @click="scheduleView = 'calendar'" :class="['px-3 py-1.5 text-xs rounded-lg font-medium', scheduleView === 'calendar' ? 'bg-blue-600 text-white' : 'bg-white border text-slate-600']">月历视图</button>
            </div>
          </div>

          <!-- 列表视图 (第四张图) -->
          <div v-if="scheduleView === 'list'" class="space-y-4">
            <div v-for="item in scheduleList" :key="item.id" class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-start justify-between">
              <div class="space-y-2">
                <div class="flex items-center gap-3">
                  <span class="text-sm font-semibold text-blue-600">{{ item.date }}</span>
                  <span class="px-2 py-0.5 text-xs bg-amber-50 text-amber-600 rounded font-medium">{{ item.type }}</span>
                </div>
                <h4 class="font-bold text-slate-800 text-base">{{ item.company }} - {{ item.title }}</h4>
                <p class="text-xs text-slate-500">📍 {{ item.location }}</p>
              </div>
              <button class="text-slate-400 hover:text-slate-600 text-xs">编辑</button>
            </div>
          </div>

          <!-- 月历视图 (第五张图) -->
          <div v-if="scheduleView === 'calendar'" class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
            <div class="grid grid-cols-7 gap-2 text-center text-xs font-semibold text-slate-400 mb-4">
              <div>一</div><div>二</div><div>三</div><div>四</div><div>五</div><div>六</div><div>日</div>
            </div>
            <div class="grid grid-cols-7 gap-2 h-96">
              <div v-for="day in 35" :key="day" class="border border-slate-100 rounded-lg p-1 text-xs relative hover:bg-slate-50">
                <span class="text-slate-400">{{ day <= 30 ? day : day - 30 }}</span>
                <div v-if="day === 16" class="mt-1 p-1 bg-blue-50 text-blue-600 rounded text-[10px] truncate">
                  14:00 绿盟科技宣讲
                </div>
                <div v-if="day === 20" class="mt-1 p-1 bg-amber-50 text-amber-600 rounded text-[10px] truncate">
                  19:00 米哈游在线笔试
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 侧边栏导航配置
const navItems = [
  { id: 'jobs', label: '27届校招', badge: '13778' },
  { id: 'assistant', label: '求职助理', badge: '' },
  { id: 'mailbox', label: '招聘邮箱', badge: '39' },
  { id: 'schedule', label: '日程安排', badge: '6' }
]

const activeTab = ref('jobs')
const scheduleView = ref('list')

// 模拟数据：岗位列表
const jobsList = ref([
  { id: 1, company: '字节跳动', title: '商业化 AI 产品经理', department: '商业化 AILab', score: 94, location: '北京/上海', platform: '官网' },
  { id: 2, company: '字节跳动', title: '大模型创新业务技术研究与落地 (Agent)', department: 'GMT Team', score: 91, location: '北京', platform: '官网' },
  { id: 3, company: '腾讯', title: '数据分析/商业分析师', department: 'IEG 事业群', score: 88, location: '深圳', platform: '官网' }
])

// 模拟数据：历史对话
const chatHistory = ref([
  { id: 1, title: '评估字节AI产品经理岗位匹配度' },
  { id: 2, title: '优化财务数据分析实习经历' }
])

// 模拟数据：邮件列表
const mailList = ref([
  { id: 1, tag: '笔试通知', title: '件云科技 2027 校招笔试通知', sender: ' hr@jianyun.com', time: '2026/09/16' },
  { id: 2, tag: '笔试通知', title: '【miHoYo】米哈游邀请你参加在线笔试', sender: ' recruitment@mihoyo.com', time: '2026/09/15' }
])

// 模拟数据：日程列表
const scheduleList = ref([
  { id: 1, date: '2026/09/16 14:00', type: '宣讲会', company: '绿盟科技', title: '2027校招宣讲会', location: '线上会议 / 2415教室' },
  { id: 2, date: '2026/09/20 19:00', type: '笔试', company: '米哈游', title: '参加专业笔试', location: '线上笔试平台' }
])
</script>