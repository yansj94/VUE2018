<template>
    <svg/>
</template>

<script>
/*eslint-disable */
import * as d3 from 'd3';
export default {
    name:'FDG',
    data() {
        return{
            nodes : [
                    { name: "Java" },
                    { name: "Web应用服务器" },
                    { name: "JDBC" },
                    { name: "框架" },
                    { name: "日志框架" },
                    { name: "JSF" },
                    { name: "JSF" }
                    ],
            edges : [
                    { source: 0, target: 1 },
                    { source: 0, target: 2 },
                    { source: 0, target: 3 },
                    { source: 3, target: 4 },
                    { source: 3, target: 5 },
                    { source: 5, target: 6 }
                    ],
         
            width:500,
            height:500
        };
    },
    mounted(){
        this.drawforce();
    },
    methods: {
        drawforce(){
            var nodes=this.nodes;
            var edges=this.edges;
            var width=this.width;
            var height=this.height;
            var svg=d3.select("svg").attr('width',width).attr('height',height);
            var force=d3.layout.force().nodes(nodes).links(edges).size([width,height]).linkDistance(100).charge(-400);
            force.start();
            var svg_edges=svg.selectAll("line").data(edges).enter().append('line').style("stroke","#ccc").style("stroke-width",1);
            var color=d3.scale.category20();
            var svg_nodes=svg.selectAll("circle").data(nodes).enter().append("circle").attr("r",20).style("fill",function(d,i){ return color(i);}).call(force.drag);
            var svg_texts=svg.selectAll("text").data(nodes).enter().append("text").style("fill","black").attr("dx",20).attr("dy",8).text(function(d){return d.name+'new';});
        
             force.on("tick",function(){
            //更新连线坐标
			     svg_edges.attr("x1",function(d){ return d.source.x; })
			 		.attr("y1",function(d){ return d.source.y; })
			 		.attr("x2",function(d){ return d.target.x; })
			 		.attr("y2",function(d){ return d.target.y; });
			 
			 //更新节点坐标
			     svg_nodes.attr("cx",function(d){ return d.x; })
			 		.attr("cy",function(d){ return d.y; });

			 //更新文字坐标
                svg_texts.attr("x", function(d){ return d.x; })
                    .attr("y", function(d){ return d.y; });
            });
        }
    }
}
</script>
