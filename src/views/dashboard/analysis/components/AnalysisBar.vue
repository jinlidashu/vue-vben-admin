<script lang="tsx">
  import { defineComponent, onMounted, ref, Ref } from 'compatible-vue';

  import { useCharts } from '@/hooks/functions/useCharts';

  import { basicProps, BasicProps } from './props';
  export default defineComponent({
    name: 'AnalysisLine',
    props: basicProps,
    setup(props: BasicProps) {
      const chartRef = ref<HTMLDivElement | null>(null);
      const { setOptions } = useCharts(chartRef as Ref<HTMLDivElement>);

      onMounted(() => {
        setOptions({
          tooltip: {
            trigger: 'axis',
            backgroundColor: 'rgba(0, 0, 0, .6)',
            axisPointer: {
              // 坐标轴指示器，坐标轴触发有效
              type: 'shadow', // 默认为直线，可选为：'line' | 'shadow'
            },
          },
          legend: {
            itemWidth: 15,
            right: 10,
            data: ['产品一', '产品二', '产品三'],
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true,
          },
          xAxis: [
            {
              type: 'category',
              axisTick: {
                inside: true, // 刻度朝内
              },
              data: ['付费用户', '免费用户', '自主'],
            },
          ],
          yAxis: [
            {
              type: 'value',
              axisTick: {
                inside: true, // 刻度朝内
              },
            },
          ],
          series: [
            {
              name: '产品一',
              type: 'bar',
              itemStyle: {
                color: '#3ca0f6',
              },
              data: [3200, 3320, 3010],
              animationDuration: 4000,
            },
            {
              name: '产品二',
              type: 'bar',
              itemStyle: {
                color: '#7dd9b9',
              },
              data: [1200, 2600, 1010],
              animationDuration: 4000,
            },

            {
              name: '产品三',
              type: 'bar',
              itemStyle: {
                color: '#e6a23c',
              },
              data: [862, 2500, 964],
              animationDuration: 4000,
            },
          ],
        });
      });

      return () => {
        const { width, height } = props;
        return <div ref={chartRef} style={{ height: height, width: width }} />;
      };
    },
  });
</script>
